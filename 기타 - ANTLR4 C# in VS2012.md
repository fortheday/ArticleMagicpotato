# [Setting Up ANTLR4 C# Target in Visual Studio 2012](https://groups.google.com/forum/#!topic/antlr-discussion/Gh_P6IiDrKU)

> VisualStudio, C# 환경에서 antlr을 빌드할 때 `Unknown build error: Could not locate a Java installation.` 같은 에러를 접하게 된다. (자바가 있는데도) 그와 관련된 도움이 되는 글이다.


This is a (revised) attempt at a full summary of the steps needed to get ANTLR4 to generate a C# lexer, parser, and listener for a very simple grammar. The C# target is designed to work as a Visual Studio (VS) add-in only and cannot be used from the command line.

Terence Parr is the author of ANTLR and Sam Harwell is the author of the C# language target for ANTLR. Any errors in this document are mine alone.

STEP 1

Goal: A working Java RE installation and creation of the registry entries the ANTLR4 C# target uses to locate the java.exe executable.

* Install the Java JRE (http://java.com/en/download/manual.jsp )
* Run regedit and examine the HKEY_LOCAL_MACHINE\SOFTWARE key. It should contain a “JavaSoft” subkey:

HKEY_LOCAL_MACHINE\SOFTWARE\JavaSoft.
I run Windows 7 64-bit. I found the above registry key was only created when I manually installed the 64-bit version of the JRE. It was no created by the 32-bit installer or the installer that runs when you click on the “Free Java Download” button on the java.com page.

The ANTLR4 C# target, needs the java runtime, and will not run without this registry key, so keep installing versions of java till you get one.

Note: Sam says that you should be able to install the 32-bit JDK on a 64-bit system and, so long as you tell the installer to install the JRE as well, the ANTLR4 C# Target will find the java runtime.

STEP 2

Goal: ANTLR Language Support extension installed in VS.

* Install ANTLR Language Support extension (a vsix file):

 http://visualstudiogallery.msdn.microsoft.com/25b991db-befd-441b-b23b-bb5f8d07ee9f
 
STEP 3
Goal: NuGet package manager at version 2.5 or greater.

* Run Visual Studio 2012.

* Click on Tools -> Extensions and Updates in the menu.
* Select Updates -> Visual Studio Gallery in the left hand panel.
* If the NuGet Paakage Manager appears, click the update button. (In my case it updated from version 2.2.40116.9051 to 2.6.40627.9000). Your goal is to get a NuGet version of 2.5 or more.
* Restart Visual Studio.
STEP 4

Goal: A VS solution and project.

* Run Visual Studio 20120

* Create a new solution called ANTLR4 with a new Console Application project in it called Hello.
STEP 5

Goal: ANTLR4 NuGet package installed in Hello project.

* In Solution Explorer, right click the Hello project folder and select “Manage NuGet Packages” in the context menu. A dialog pops up.

* In the left hand panel select “NuGet official package source”.
* At the top select “Include Prerelease” in the left hand combo box.
* In the search panel at top right type “ANTLR4”.
* The “ANTLR 4” package will appear in the central list. Install it.
This package must be installed in each project that uses the ANTLR C# target.

STEP 6

Goal: A simple ANTLR Grammar.

* In Solution Explorer, right click the Hello project folder and select “Add -> New Item” in the context menu. A dialog pops up.

* Select Visual C# Items -> ANTLR in the left hand panel.
* Select “ANTLR4 Combined Grammar” in the central panel.
* Enter the name “Hello.g4” at the bottom.
* Click the Add Button.
* Open the Hello.g4 file and replace all its text with the following:
 grammar Hello;

 HELLOWORD : 'hello' ;

 r  : HELLOWORD ID ;         // match keyword hello followed by an identifier
 ID : [a-z]+ ;              // match lower-case identifiers

 WS : [ \t\r\n]+ -> skip ;
STEP 7

Goal: A program to parse the Hello.g4 grammar, parse a text string, and traverse the parsed tokens.

* Create a new class called MyVisitor  as follows:

    public class MyVisitor : HelloBaseVisitor<object> {

 
        public override object VisitR([NotNull] HelloParser.RContext context) {
            Console.WriteLine("HelloVisitor VisitR");
            context
                .children
                .OfType<TerminalNodeImpl>()
                .ToList()
                .ForEach(child => Visit(child));
            return null;
        }
  
        private void Visit(TerminalNodeImpl node) {
            Console.WriteLine(" Visit Symbol={0}", node.Symbol.Text);
        }
    }
 
* Open the Program.cs file.

* Add the following using statement at the top of the file:
 using Antlr4.Runtime;

* Replace all the class text with the following:

    class Program {

        private static void Main(string[] args) {
            (new Program()).Run();
        }
        public void Run() {

            try {
                Console.WriteLine("START");
                RunParser();
                Console.Write("DONE. Hit RETURN to exit: ");
            } catch (Exception ex) {
                Console.WriteLine("ERROR: " + ex);
                Console.Write("Hit RETURN to exit: ");
            }
            Console.ReadLine();
        }
        private void RunParser() {

            AntlrInputStream inputStream = new AntlrInputStream("hello world\n");
            HelloLexer helloLexer = new HelloLexer(inputStream);
            CommonTokenStream commonTokenStream = new CommonTokenStream(helloLexer);
            HelloParser helloParser = new HelloParser(commonTokenStream);
            HelloParser.RContext rContext = helloParser.r();
            MyVisitor visitor = new MyVisitor();
            visitor.VisitR(rContext);
        }
    }
 
If you have ReSharper installed you will probably see syntax errors reported by intellisense in AddParseListener and RContext. These are, according to Sam, due to a bug in ReSharper. Ignore the “errors” for now or disable ReSharper via the Tools -> Options -> ReSharper -> General tab.

* Build the program. It should build successfully.

STEP 8

Goal: Run the program with the expected result.

* Run the Hello program.

* You should see the following output in the console window:
 
 START

 HelloVisitor VisitR
 Visit Symbol=hello
 Visit Symbol=world
 DONE. Hit RETURN to exit:
 
The program parsed the text “hello world” and chopped it up into 2 terminal tokens, as you can see above.

STEP 9

Goal: Understand how it works (only a bit though).

* Look in the ANTLR4\Hello\obj\Debug directory and observe the following files:

 HelloBaseListener.cs

 HelloBaseVisitor.cs
 HelloLexer.cs
 HelloLexer.tokens
 HelloListener.cs
 HelloParser.cs
 HelloVisitor.cs
 
USEFUL LINKS

http://antlr.org/

http://tunnelvisionlabs.com/products/demo/antlrworks
 
ATTACHED FILES
 
A word file with this text in it.
A zip file of the Visual Studio Hello project. This should be placed in a solution directory and would be accompanied by a packages directory containing Antlr4.4.1.0-alpha003 and Antlr4.Runtime.4.1.0-alpha003 which are got from NuGet.
