# CBT761
Converted to GitHub via [cbt2git](https://github.com/wizardofzos/cbt2git)

This is still a work in progress. GitHub repos will be deleted and created during this period...

```
//***FILE 761 is from Mark Baron and contains several REXX execs    *   FILE 761
//*           which help you to find things on an MVS system.       *   FILE 761
//*           The name of the principal REXX exec, and the name     *   FILE 761
//*           of the package itself is FINDALL.                     *   FILE 761
//*                                                                 *   FILE 761
//*       email:  Mark Baron <msb1230@optonline.net>                *   FILE 761
//*                                                                 *   FILE 761
//*     Contents of this file:                                      *   FILE 761
//*                                                                 *   FILE 761
//*      FINDALL  - REXX EXEC to scan the user's ISPLLIB,           *   FILE 761
//*                 STEPLIB, the LPALIST, the LINKLIST, the         *   FILE 761
//*                 user's SYSPROC, and SYSEXEC concatenations      *   FILE 761
//*                 for the specified member.  Calling              *   FILE 761
//*                 sequence:                                       *   FILE 761
//*                                                                 *   FILE 761
//*                     FINDALL member {listtype}                   *   FILE 761
//*                             member is the program command       *   FILE 761
//*                                    CLIST or REXX to be          *   FILE 761
//*                                    located                      *   FILE 761
//*                             listtype is either the word         *   FILE 761
//*                                      SHORT (default) or         *   FILE 761
//*                                      LONG.  SHORT will          *   FILE 761
//*                                      display only the           *   FILE 761
//*                                      library containing an      *   FILE 761
//*                                      instance of member.        *   FILE 761
//*                                      LONG will display the      *   FILE 761
//*                                      entire list with the       *   FILE 761
//*                                      the status from SYSDSN.    *   FILE 761
//*                                                                 *   FILE 761
//*      FINDPAN  - REXX EXEC to scan the user's ISPPLIB            *   FILE 761
//*                 concatenation for the specified ISPF panel.     *   FILE 761
//*                 The calling sequence is the same as for         *   FILE 761
//*                 FINDALL.                                        *   FILE 761
//*                                                                 *   FILE 761
//*      FINDPARM - REXX EXEC to scan the system PARMLIB            *   FILE 761
//*                 concatenation for the specified parm member.    *   FILE 761
//*                 The parmlib concatenation is built from the     *   FILE 761
//*                 information stored in the IPA during IPL.       *   FILE 761
//*                 The calling sequence is the same as for         *   FILE 761
//*                 FINDALL.                                        *   FILE 761
//*                                                                 *   FILE 761
//*      FINDPROC - REXX EXEC to scan the JES2 PROCLIB              *   FILE 761
//*                 concatenation(s) for the specified PROC. The    *   FILE 761
//*                 proclib concatenation must be built manually    *   FILE 761
//*                 from the JES2 JCL since I was too lazy to       *   FILE 761
//*                 write code to go cross memory to JES2 to get    *   FILE 761
//*                 it from the $HCT.  (If anyone has some code     *   FILE 761
//*                 to do this, please feel free to share it        *   FILE 761
//*                 with me and I will incorporate it into the      *   FILE 761
//*                 EXEC.)The calling sequence is the same as       *   FILE 761
//*                 for FINDALL.                                    *   FILE 761
//*                                                                 *   FILE 761
//*      #FINDLPA - REXX EXEC subroutine to extract the LPALST      *   FILE 761
//*                 dataset names from the LPAT.  The LPA           *   FILE 761
//*                 libraries are not allocated except as might     *   FILE 761
//*                 occur for SYSDSN processing.  The EXEC is       *   FILE 761
//*                 written so as to function as either a           *   FILE 761
//*                 subroutine or as a main program.  If invoked    *   FILE 761
//*                 as a main program, it will stop at the first    *   FILE 761
//*                 occurrence of the target member and ask if      *   FILE 761
//*                 the user wants to continue scanning the rest    *   FILE 761
//*                 of the LPALST libraries.  The calling           *   FILE 761
//*                 sequence is the same as for FINDALL.            *   FILE 761
//*                                                                 *   FILE 761
//*      #FINDMOD - REXX EXEC subroutine to extract the LINKLIST    *   FILE 761
//*                 dataset names from the caller's Link List       *   FILE 761
//*                 Set.  The Link List libraries are not           *   FILE 761
//*                 allocated except as might occur for SYSDSN      *   FILE 761
//*                 processing.  The EXEC is written so as to       *   FILE 761
//*                 function as either a subroutine or as a main    *   FILE 761
//*                 program.  If invoked as a main program, it      *   FILE 761
//*                 will stop at the first occurrence of the        *   FILE 761
//*                 target member and ask if the user wants to      *   FILE 761
//*                 continue scanning the rest of the LPALST        *   FILE 761
//*                 libraries.  The calling sequence is the same    *   FILE 761
//*                 as for FINDALL.                                 *   FILE 761
//*                                                                 *   FILE 761
//*      #GENFIND - REXX EXEC subroutine to scan the output of      *   FILE 761
//*                 LISTA STA to find the target DDName             *   FILE 761
//*                 concatenation and then to scan for the          *   FILE 761
//*                 target member.  Calling sequence:               *   FILE 761
//*                    #GENFIND ddname member {listtype}            *   FILE 761
//*                             ddname is the target                *   FILE 761
//*                             concatenation                       *   FILE 761
//*                             member is the element to be         *   FILE 761
//*                             located                             *   FILE 761
//*                             listtype is either the word         *   FILE 761
//*                                      SHORT (default) or         *   FILE 761
//*                                      LONG.  SHORT will          *   FILE 761
//*                                      display only the           *   FILE 761
//*                                      library containing an      *   FILE 761
//*                                      instance of member.        *   FILE 761
//*                                      LONG will display the      *   FILE 761
//*                                      entire list with the       *   FILE 761
//*                                      the status from SYSDSN.    *   FILE 761
//*                                                                 *   FILE 761
//*      #SYSID   - REXX EXEC subroutine extract the System name    *   FILE 761
//*                 from CVTSNAME.  If called as subroutine, it     *   FILE 761
//*                 will simply return the system name.  If         *   FILE 761
//*                 called as a standalone commands is will         *   FILE 761
//*                 display it.  There are no parms in the          *   FILE 761
//*                 calling sequence                                *   FILE 761
//*                                                                 *   FILE 761
//*      $$README - A short note about compatibility.               *   FILE 761
//*                                                                 *   FILE 761
//*      $INSTALL - A note on where to put these things in order    *   FILE 761
//*                 to run them.                                    *   FILE 761
//*                                                                 *   FILE 761
//*      Mark Baron - msb1230@optonline.net                         *   FILE 761
//*                                                                 *   FILE 761
```
