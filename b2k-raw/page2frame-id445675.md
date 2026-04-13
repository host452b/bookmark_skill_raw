// 1 filename: Te_td_sqrt1.cpp

// ver 0.1 15(Sat), Oct, 2017

#include &lt;iostream&gt;

#include &lt;string&gt;

#include &lt;cstdlib&gt;

// 2 original examples and/or notes:

// (c) Copyright 2003 "C++ Templates - The Complete Guide" by Pearson Education, Inc. David Vandevoorde, and Nicolai M. Josuttis.  All rights reserved.

// http://www.josuttis.com/tmplbook/

// The best way to reach the author of the book is by e-mail:tmplbook@josuttis.com

std::string ru ("\"C++ Templates Part III: Templates and Design.\"");

std::string rus ("\"Chapter 17. Metaprograms 17.3 A Second Example: Computing the Square Root, Te_td_sqrt1.cpp \"");

// 3 compile and output mechanism:

// (c) Dr. OGAWA Kiyoshi, twitter @kaizen_nagoya e-mail:kaizen at wh.commufa.jp

// https://researchmap.jp/jo0n1csau-1797580/#_1797580

// [https://researchmap.jp/jo08bcs4r-49935/#_49935](https://researchmap.jp/jo08bcs4r-49935/#_49935)

 clang++ no warning, g++ 1 warning(many)

//

// 4 compile errors and/or warnings:

// 4.1  Clang  http://www.llvm.org/

// Copyright (c) 2003-2017, LLVM Project

// clang++ --version

// (c) clang version 5.0.0 (tags/RELEASE_500/final)

// Target: x86_64-apple-darwin14.5.0

// Thread model: posix

// InstalledDir: /usr/local/opt/llvm/bin

// Base standard: https://clang.llvm.org/cxx_status.html

// Command/Options: clang++ -std=c++17 -stdlib=libc++ -Wall Te_td_sqrt1.cpp -o  Te_td_sqrt1L

// Configuration: brew install --with-clang llvm

//

// 4.2. g++ (Homebrew GCC 6.4.0) 6.4.0

// Copyright (C) 2017 Free Software Foundation, Inc.

// This is free software; see the source for copying conditions.

// There is NO warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

// ln -s /usr/local/bin/gcc-6 /usr/local/bin/gcc

// ln -s /usr/local/bin/g++-6 /usr/local/bin/g++

// Base standard: http://gcc.gnu.org/onlinedocs/gcc/Standards.html

// Command/Options: g++  -std=c++17  -Wall  Te_td_sqrt1.cpp  -o  Te_td_sqrt1G

// Configuration:brew install gcc6

//

// 5. Hardware:  MacBook Pro,  (Retina, 13-inch, Mid 2014)

// OS X 10.10.5 Yosemite

//Core i5, 2.6GHz, 16GB, 1600MHz DDR3

//(c) Intel http://ark.intel.com/products/series/75024/4th-Generation-Intel-Core-i5-Processors

//

// 6. Special Thanks: Upper organizatios and

// ISO/IEC JTC1 SC22 WG21: http://www.open-std.org/jtc1/sc22/wg21/

// MISRA: https://www.misra.org.uk/forum/index.php

// CERT: https://www.securecoding.cert.org/

// ISO/IEC JTC1 SC22 WG14: http://www.open-std.org/jtc1/sc22/wg14/

// ITSCJ/IPSJ http://www.itscj.ipsj.or.jp/itscj_english/index.html

// Renesas Electronics Corporation.http://www.renesas.com/

// NPO SESSAME project, http://www.sessame.jp/workinggroup/WorkingGroup3/

// Toyo Corporation, http://www.toyo.co.jp/English/

// Japan Standard Association, http://bit.ly/1lzykg1

// NPO TOPPERS project, https://www.toppers.jp/asp-d-download.html

// Daido Universcity, http://www.daido-it.ac.jp/gakubugakka/computer/index.html

// WITZ Co.Ltd., http://www.witz-inc.co.jp/products/solution/solution.html

// SevenWise.Co., http://www.7ws.co.jp/index.html

// TOYOTA Motor Corporation, http://toyota.jp/

// DENSO Corporation, http://www.globaldenso.com/en/

// Aisin Seiki Co. Ltd., http://www.aisin.com/

// Cypress Semiconductor Corp., http://japan.cypress.com/

// Yazaki Corporation, http://www.yazaki-group.com/global/

// Pananosic Corporation, http://www.panasonic.net/

// Denso Create Inc.: http://www.denso-create.jp

// SWEST: Summer Workshop on Embedded System Technologies , http://swest.toppers.jp

// CEST: Consortium for Embedded System Technology, http://www.ertl.jp/CEST/

// JUSE: Union of Japanese Scientists and Engineers, http://www.juse.or.jp/e/

// OSC: Open Source Conference, http://www.ospn.jp/

// 7. notes

//{T} C++ Templates - The Complete Guide

//{L} LLVM warnings and errors

//{G} Gcc warning and errors

//{S} C++ standard, ISO/IEC JTC1 SC22 WG14

// add 'n' to function and variable names of non compliant example if a same name exists. And sequence number also.

// add 'c' to  function and variable names of compliant examples if a same name exists. And sequence number also.

// 8. source code

/// Begining 3 slash code is comment out for avoiding ERROR.

/// After code, with 3 slash is added something by DR. O.K., or is not original source code.

//{T} 

/* The following code example is taken from the book

 * "C++ Templates - The Complete Guide"

 * by David Vandevoorde and Nicolai M. Josuttis, Addison-Wesley, 2002

 *

 * (C) Copyright David Vandevoorde and Nicolai M. Josuttis 2002.

 * Permission to copy, use, modify, sell and distribute this software

 * is granted provided this copyright notice appears in all copies.

 * This software is provided "as is" without express or implied

 * warranty, and with no claim as to its suitability for any purpose.

*/

// ./meta/sqrt1.cpp

#include "sqrt1.hpp"

int main(int argc, char* argv[])/// add argc and argv

{

    std::cout &lt;&lt; "// "  &lt;&lt; "Sqrt&lt;16&gt;::result = " &lt;&lt; Sqrt&lt;16&gt;::result

              &lt;&lt; '\n';

    std::cout &lt;&lt; "// "  &lt;&lt; "Sqrt&lt;25&gt;::result = " &lt;&lt; Sqrt&lt;25&gt;::result

              &lt;&lt; '\n';

    std::cout &lt;&lt; "// "  &lt;&lt; "Sqrt&lt;42&gt;::result = " &lt;&lt; Sqrt&lt;42&gt;::result

              &lt;&lt; '\n';

    std::cout &lt;&lt; "// "  &lt;&lt; "Sqrt&lt;1&gt;::result =  " &lt;&lt; Sqrt&lt;1&gt;::result

              &lt;&lt; '\n';    

    std::cout &lt;&lt; "// " &lt;&lt; ru &lt;&lt; std::endl &lt;&lt;"// " &lt;&lt; rus &lt;&lt; std::endl ;///

    return argc; ///

}

// 9 Error, Warning and/or Output using Te.sh script: ../Te.sh program_name

// 9.1 clang++(LLVM) 

// Sqrt&lt;16&gt;::result = 4

// Sqrt&lt;25&gt;::result = 5

// Sqrt&lt;42&gt;::result = 6

// Sqrt&lt;1&gt;::result =  1

// "C++ Templates Part III: Templates and Design."

// "Chapter 17. Metaprograms 17.3 A Second Example: Computing the Square Root, Te_td_sqrt1.cpp "

// Te_td_sqrt1.cpp clang++ OK!

//

// 9.2 g++(GCC) 

//In file included from Te_td_sqrt1.cpp:95:0:

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;16, 1, 2&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;16, 1, 8&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;16&gt;'

//Te_td_sqrt1.cpp:99:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;16, 1, 1&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;16, 2, 2&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//

//                     ~~~~~~~~~~~~^~~~~~~~~~~~~~~~~~~~~~~~~~~

//                                 : Sqrt&lt;N,mid,HI&gt;::result };

//                                 ~~~~~~~~~~~~~~~~

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;16, 3, 4&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;16, 1, 8&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;16&gt;'

//Te_td_sqrt1.cpp:99:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;16, 3, 3&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;16, 4, 4&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;16, 1, 4&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;16, 1, 8&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;16&gt;'

//Te_td_sqrt1.cpp:99:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;16, 1, 2&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;16, 3, 4&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;16, 5, 6&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;16, 1, 8&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;16&gt;'

//Te_td_sqrt1.cpp:99:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;16, 5, 5&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;16, 6, 6&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;16, 7, 8&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;16, 1, 8&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;16&gt;'

//Te_td_sqrt1.cpp:99:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;16, 7, 7&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;16, 8, 8&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;16, 5, 8&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;16, 1, 8&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;16&gt;'

//Te_td_sqrt1.cpp:99:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;16, 5, 6&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;16, 7, 8&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;16, 1, 8&gt;':

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;16&gt;'

//Te_td_sqrt1.cpp:99:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;16, 1, 4&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;16, 5, 8&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;16, 9, 10&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;16, 9, 16&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;16&gt;'

//Te_td_sqrt1.cpp:99:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;16, 9, 9&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;16, 10, 10&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;16, 11, 12&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;16, 9, 16&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;16&gt;'

//Te_td_sqrt1.cpp:99:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;16, 11, 11&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;16, 12, 12&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;16, 9, 12&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;16, 9, 16&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;16&gt;'

//Te_td_sqrt1.cpp:99:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;16, 9, 10&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;16, 11, 12&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;16, 13, 14&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;16, 9, 16&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;16&gt;'

//Te_td_sqrt1.cpp:99:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;16, 13, 13&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;16, 14, 14&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;16, 15, 16&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;16, 9, 16&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;16&gt;'

//Te_td_sqrt1.cpp:99:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;16, 15, 15&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;16, 16, 16&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;16, 13, 16&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;16, 9, 16&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;16&gt;'

//Te_td_sqrt1.cpp:99:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;16, 13, 14&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;16, 15, 16&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;16, 9, 16&gt;':

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;16&gt;'

//Te_td_sqrt1.cpp:99:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;16, 9, 12&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;16, 13, 16&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;16&gt;':

//Te_td_sqrt1.cpp:99:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;16, 1, 8&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;16, 9, 16&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 2, 3&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;25, 1, 12&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 2, 2&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 3, 3&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 1, 3&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;25, 1, 12&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 1, 1&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 2, 3&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 5, 6&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;25, 1, 12&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 5, 5&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 6, 6&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 4, 6&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;25, 1, 12&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 4, 4&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 5, 6&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 1, 6&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;25, 1, 12&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 1, 3&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 4, 6&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 8, 9&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;25, 1, 12&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 8, 8&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 9, 9&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 7, 9&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;25, 1, 12&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 7, 7&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 8, 9&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 11, 12&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;25, 1, 12&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 11, 11&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 12, 12&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 10, 12&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;25, 1, 12&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 10, 10&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 11, 12&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 7, 12&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;25, 1, 12&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 7, 9&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 10, 12&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 1, 12&gt;':

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 1, 6&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 7, 12&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 14, 15&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;25, 13, 25&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 14, 14&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 15, 15&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 13, 15&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;25, 13, 25&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 13, 13&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 14, 15&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 17, 18&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;25, 13, 25&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 17, 17&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 18, 18&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 16, 18&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;25, 13, 25&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 16, 16&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 17, 18&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 13, 18&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;25, 13, 25&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 13, 15&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 16, 18&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 20, 21&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;25, 13, 25&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 20, 20&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 21, 21&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 19, 21&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;25, 13, 25&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 19, 19&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 20, 21&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 22, 23&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;25, 13, 25&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 22, 22&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 23, 23&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 24, 25&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;25, 13, 25&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 24, 24&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 25, 25&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 22, 25&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;25, 13, 25&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 22, 23&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 24, 25&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 19, 25&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;25, 13, 25&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 19, 21&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 22, 25&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25, 13, 25&gt;':

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;25&gt;'

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 13, 18&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 19, 25&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;25&gt;':

//Te_td_sqrt1.cpp:101:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;25, 1, 12&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;25, 13, 25&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 1, 2&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 1, 21&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 1, 1&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 2, 2&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 4, 5&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 1, 21&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 4, 4&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 5, 5&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 3, 5&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 1, 21&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 3, 3&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 4, 5&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 1, 5&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 1, 21&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 1, 2&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 3, 5&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 6, 7&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 1, 21&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 6, 6&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 7, 7&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 9, 10&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 1, 21&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 9, 9&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 10, 10&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 8, 10&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 1, 21&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 8, 8&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 9, 10&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 6, 10&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 1, 21&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 6, 7&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 8, 10&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 1, 10&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 1, 21&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 1, 5&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 6, 10&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 11, 12&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 1, 21&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 11, 11&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 12, 12&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 14, 15&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 1, 21&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 14, 14&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 15, 15&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 13, 15&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 1, 21&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 13, 13&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 14, 15&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 11, 15&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 1, 21&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 11, 12&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 13, 15&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 17, 18&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 1, 21&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 17, 17&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 18, 18&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 16, 18&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 1, 21&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 16, 16&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 17, 18&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 20, 21&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 1, 21&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 20, 20&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 21, 21&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 19, 21&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 1, 21&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 19, 19&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 20, 21&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 16, 21&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 1, 21&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 16, 18&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 19, 21&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 11, 21&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 1, 21&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 11, 15&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 16, 21&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 1, 21&gt;':

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 1, 10&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 11, 21&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 22, 23&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 22, 42&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 22, 22&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 23, 23&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 25, 26&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 22, 42&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 25, 25&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 26, 26&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 24, 26&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 22, 42&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 24, 24&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 25, 26&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 22, 26&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 22, 42&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 22, 23&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 24, 26&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 27, 28&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 22, 42&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 27, 27&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 28, 28&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 30, 31&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 22, 42&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 30, 30&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 31, 31&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 29, 31&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 22, 42&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 29, 29&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 30, 31&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 27, 31&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 22, 42&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 27, 28&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 29, 31&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 22, 31&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 22, 42&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 22, 26&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 27, 31&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 32, 33&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 22, 42&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 32, 32&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 33, 33&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 35, 36&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 22, 42&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 35, 35&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 36, 36&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 34, 36&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 22, 42&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 34, 34&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 35, 36&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 32, 36&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 22, 42&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 32, 33&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 34, 36&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 38, 39&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 22, 42&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 38, 38&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 39, 39&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 37, 39&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 22, 42&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 37, 37&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 38, 39&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 41, 42&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 22, 42&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 41, 41&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 42, 42&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 40, 42&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 22, 42&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 40, 40&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 41, 42&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 37, 42&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 22, 42&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 37, 39&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 40, 42&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 32, 42&gt;':

//sqrt1.hpp:22:33:   recursively required from 'class Sqrt&lt;42, 22, 42&gt;'

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 32, 36&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 37, 42&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42, 22, 42&gt;':

//sqrt1.hpp:22:33:   required from 'class Sqrt&lt;42&gt;'

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 22, 31&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 32, 42&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

//sqrt1.hpp: In instantiation of 'class Sqrt&lt;42&gt;':

//Te_td_sqrt1.cpp:103:61:   required from here

//sqrt1.hpp:22:33: warning: enumeral mismatch in conditional expression: 'Sqrt&lt;42, 1, 21&gt;::&lt;anonymous enum&gt;' vs 'Sqrt&lt;42, 22, 42&gt;::&lt;anonymous enum&gt;' [-Wenum-compare]

// Sqrt&lt;16&gt;::result = 4

// Sqrt&lt;25&gt;::result = 5

// Sqrt&lt;42&gt;::result = 6

// Sqrt&lt;1&gt;::result =  1

// "C++ Templates Part III: Templates and Design."

// "Chapter 17. Metaprograms 17.3 A Second Example: Computing the Square Root, Te_td_sqrt1.cpp "

// Te_td_sqrt1.cpp g++ OK!