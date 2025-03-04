
# TU SIF Fixed Income Analysis Documentation

## Introduction

This documentation is meant to educate, inform, and document the concepts and steps taken to create this project. The Fixed Income Analysis application is writed in python and coded by Ian Bates as part of a graduate project for the the University of Tulsa's fixed income seminar for the purpose of illustrating and providing insight into yields, yield curves, bonds, and bond valuation. As such, this documentation is provided for users and future contributors of this project.

This documentation will cover 3 major sections: the fixed income concecpts required to understand the project, how to use the application, and the python code and steps taken to create the project deliverables.

#### Inspiration and References
The inspriration for this project was the CFA level 2 Fixed Income curriculum and is the source of the initial bond valuation concepts. This is further supplemented by *The Handbook of Fixed Income Securities* by Fabozzi, Statistical Analysis of Financial Data in R by Rene Carmona, 

## Fixed Income Concepts


#### Yields

There are serveral core yields that are important to understand in fixed income, we will focus on these four: yield to maturity (YTM), par (coupon*), spot (zero), and forward.

The **yield to maturity** is the yield you are likely most familiar with, as it is commonly used in the present value formula: *N*, *I*, *PV*, *PMT*, *FV*; the *I* represents the yield to maturity and is expressed in this formula:

It is clear from this formula that the yield to maturity is a discount rate. It is the rate used to discount the cashflow and is compounded as a function of time. However, for each period it is a constant rate, which may not be an accurate portrayal of what we ussually witness in real life.

In **yield curve** is the collection of yield rates over various periods of time. In normal (positive) economic conditions, the yield curve is upward sloping.

The **par yield** is the yield to maturity of a bond issued at par. This means that the bond's coupon rate is the same as the yield to maturity.
The OIS curve is a par curve: a series of par yields for different periods. The OIS curve is comprised of overnieght indexed swaps, which are plain vinilla interest rate swaps. This means that someone is agreeing to swap payments on some notional amount (lets say 1 million), where there is one fixed rate payer (4%) and one floating rate payer (Overnight Index Rates). So during the stipulated payment periods, they each exchange payments, the fixed rate payer always gives the same amount (40,000) and the floating rate payer always gives whatever the overnight index rate dictates (if 2% then 20,000).

The **spot yield** or **zero yield** is the yield to maturity of a bond with zero coupons. This yield can be bootstrapped from the par yields on benchmark bonds. The formula for the spot yield is derived from:


The **forward yield** is the relatively simpler. The forward yield is the yield that would be the spot yield from some point in time. Thus if we know what the spot yields are today we can derive what the expected yield should be at some point in the future, knowing how compouning rates work we derive:

The European Central Bank provides the yield curves from septermber 2004 for Par, Spot, and Instantaneous Forward Rates. View this link for real world exampls over time. 
https://www.ecb.europa.eu/stats/financial_markets_and_interest_rates/euro_area_yield_curves/html/index.en.html

Look at how Europe experimented with negative rates for a number of years. What does this entail? Japan and some other countries also experimented with negative rates.

If you are wondering if it worked, look at if they still have negative rates. 

#### Binomial Tree (lattice)

Trees are common methods of organizing objects, and in the world of finance a useful tree for visualization and valuation of bonds and options. 

##### Tree

A tree is comprised of nodes. These nodes connect to each other in a heirarchicy. Each node can then lead to other nodes. A tree starts with a root node. A node that connects to another node is below that node in the heirarchy then it is a child node.  If a node has a child, then it is a parent. If a node has no children then it is a leaf node. A level represents the distance from the root node. The height of a tree is represented how many levels a tree has, and is this the furthest distance a node is from the root. 

If every node on levels 0 to height - 1 has the max number of chilren then the tree is full and balanced. If nodes can have multiple parents, then it is a recombinding tree and can be referred to as a lattice. If each node can only have a max of 2 children, then it is a binomial tree.



#### Calculations

The program works by building out an interest rates tree using the par and spot rates inputed.

The program iteratively constructs the interest rate tree by guessing what the forward rates may be and calculating the bond value through a bond value tree. If the bond value is too high, it guesses higher rates, if the bond value is too low it guesses lower interest rates. When the bond value was too high and is now too low or vice versa, the amount the interest_rates change decreases. This continues up to a precision of 4 decimal places (or however many the precision variable is set to).

The tree is organized as a multidimensional list, where each list in the tree represents a layer. The index for the children is the index of the parent and the parent + 1.

### How to use version 0.1
1. Fill out the Rates.xlsx excel fill, do not change the column names or sheet names.
2. Run the program.
3. Select the Rates.xlsx excel file.
4. Wait for the program to finish calculating.
5. Select a file output, name it however you please.
6. The program is finished, open up your output file and view the results.

## Coding and Creation
This section is written for the purpose of promoting contributons to this document and to the code base

#### Python Scripts
The scripts should hopefully be self explanitory and follow the general guidlines for object oriented programming and writing python.

If you are unfamiliar with python I have provide the general steps, but I would highly recommend you read books and the documentation for the packages you want to use. the matplotlib documentation is extensive and goes far beyond what is taught in the TU Business Analytics curriculum.

##### Get started
Download python, make sure it is added to your path environment.
For windows, download off the windows store. You can do that by running *python* in the command terminal and downloading it.

I used Visual Studio Code, you can install that by searching for it in a browser, click the download button, and run the launcher. Download the python extentions, including pylance. You can then create an environment by clicking into the top search bar and searching >Python: Create Environment. The shortcut for running commands (>) is CTRL + SHIFT + P. I used the venv environment. 

Use the terminal to download packages you want with *pip install "package"* or *python -m pip install "package"*. If those don't work, try changing directory with command *cd* into or out of venv.

Now start coding. Read documentations of the packages you use. I use matplotlib and tkinter mostly. ChatGPT is sometimes helpful, and 90% of the time wrong, if it doesn't provide code that works as intended read the documenation.

##### Building the exe
I used pyinstaller to build the distributable executable file. Nuitka is also a viable option. I had issues with anti-virus when using the pyinstaller package.
The pyinstaller package seems to bundle a python interpreter with the executable which unpackages itself when run in order to run the python code. Nuitka, I believe, converts the python code into C++ and then into machine code, which may be preferable to avoid anti-virus issues.

#### Documentation
The documenation you are reading now was written in Visual Studio Code in a Markdown file using the Markdown Preview Enhanced extension.
You can make a markdown file with the .md extension and following the markdown syntax and guidlines. Markdown files can alternatively be written in other software, and are incredibly popular and useful. Github will host these files on their Github Pages.

#### Future Contribution
There are many possible ways to contribute and build upon this project. Use Bloomberg as a reference to the scale that these applications can take. Bloomberg an amazing and extensive data source that offers products ranging from 80,000 to 1,000,000,000 and more. Bloomberg offers many products that go way beyond the scope of what the SIF needs in many cases, but they can give insight into the value that this project can provide. 

##### Bloomberg
I would love to enhance the api call capabilities of this application to the Bloomberg terminals. For future reference, there are two ways to access the bloomberg api documentation: One way is by searching for it in a browser and accessing the public api documentation, the other way is to access bloomberg's professional website using a bloomberg terminal login.
Using the bloomberg professional api documentation and resources is much preferred as they offer a more comprehensive and extensive guides, especially for python. They also offer a code guide tool that produces the code through a gui.
I would have also liked to explore the possibility of the bloomberg APP Portal partnership, which would require the hosting of a .NET application and the SDK on a bloomberg terminal. They are not insurmountable, but require admin access for TU network computers and collaboration with Bloomberg.


