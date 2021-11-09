                                     DELTA
                         Version 1.01 [April 15, 1993]
 
 
          Author:  Dr. Peter Ekstrom
                   Department of Physics
                   University of Lund
                   Solvegatan 14
                   S-223  62 Lund
                   SWEDEN
                   Phone: +46-46-107647 FAX: +46-46-104709
                   BITNET:  "GARBOPE@SELDC52"
                   INTERNET: "PETER.EKSTROM@NUCLEAT.LR.LU.SE"
 
               This program analyses  angular  correlation  and  conversion
          coefficient  data,  and  calculates  the  best  values  of mixing
          ratios.  the sign convention is that of Krane and Steffen,  Phys.
          Rev.  C2, 724 (1970).
 
               The gamma-gamma cascade studied is:
                     --------- J(1)
                         |
                         |  DELTA(1)    (TRANSITION NUMBER 1)
                         |
                         V
                     --------- J(2)
                         |                 .
                         |  DU(1)          .
                         |                 .
                         V                 .
                     --------- J(3)        .
                                           . UNOBSERVED TRANSITIONS
                     --------- J(NLEV-2)   .      (MAXIMUM 3)
                         |                 .
                         |  DU(NLEV-3)     .
                         |                 .
                         V                 .
                     --------- J(NLEV-1)
                         |
                         |  DELTA(2)    (TRANSITION NUMBER 2)
                         |
                         V
                     --------- J(NLEV)
 
          DELTA(1) and DELTA(2) can be varied.  The mixing  ratios  of  the
          unobserved transitions are fixed.  Possible data items are:
 
          1.  A(2) and A(4)  for  gamma-gamma  correlation  (corrected  for
              solid angle effects).
 
          2.  DELTA values from other independent measurements (ATAN(DELTA)
              is used internally).
 
          3.  Conversion coefficient or conversion ratio data.
 
 
 
                                       1
 
                                     DELTA
                         Version 1.01 [April 15, 1993]
 
 
               All data items are treated as independent, and uncertainties
          as statistical.  Note that a measured A(2) only gives very little
          information if  both  mixing  ratios  are  unknown.   A  measured
          internal  conversion  coefficient  helps  a lot!  Note that DELTA
          values  may  be  suspect  when  minimum  is   not   approximately
          parabolic.   The  default  step size in ATAN(DELTA) is 2 degrees.
          This is normally small enough,  but  for  very  accurate  data  a
          smaller step size (set with option ST) may be necessary.
 
          Limitations:
 
          1.  No triple correlations.
 
          2.  Spins  up  to  20  are  allowed,   except   when   unobserved
              transitions  are  involved.   for  unobserved transitions the
              maximum spin is 10.   These  limitations  are  valid  if  the
              computer can handle double precision reals of up to 10**76.
 
          3.  Effects  of  internal   conversion   on   the   deorientation
              coefficients   for  mixed  transitions  are  neglected.   See
              Anicin, et al., Nucl.   Instr.   103,  395  (1972)  for  this
              usually very small effect.
 
 
          NOTE:  Except for the changes made in input and output units  and
          to  conform  to ANSI-77 standard, this code is as provided by the
          author.
 
          Input file: All records have the following format:
                COL. 1-2  Symbol that determines type of card.
                COL. 3-72 Free format reals or integers. Separator: any
                          character different from '0-9', '.' and '-'.
                          Everything following a '$' is ignored. This
                          can be used for comments on the data cards.
                Only DATA and GO cards are necessary. Uncert.= 0 for DELTA
                means that DELTA is kept fixed. new data with same name as
                existing data replace the latter.
                Options (parameters in () are optional)
                 CL                          Clear data
                 DU                          Dump common blocks (for
                                             debugging)
                 OU A                        A=0 short output (default)
                                             A>0 FULL OUTPUT
                 ST ST1(,ST2)                Stepsize (in degrees) for
                                             ATAN(DELTA1) and ATAN(DELTA2),
                                             respectively
                 EN                          End of run
                 GO RJ1,RJ2(,RJ3)            Read spins and go. RJ are
                                             reals or integers. (e.g.,
                                             5/2-=-2.5, 2+=2, 0-=-0)
                                             Maximum 6 spins.
                 HE ANY TEXT                 Header
 
                                       2
 
                                     DELTA
                         Version 1.01 [April 15, 1993]
 
 
                 LI A,B,C,D                  Limits ATAN(DELTA1) to A to B
                                             and ATAN(DELTA2) to c to d
                 UN (DU(1),DU(2),DU(3))      Unobserved transitions,
                                             DELTAS. Defaults=0.0
                Correlation and DELTA data
                 A2 A2,DA2                   A2, uncertainty in A2
                 A4 A4,DA4                   A4, uncertainty in A4
                 D  NTR(,DELTA,DDELTA)       Transition number, DELTA,
                                             uncert. in DELTA. Defaults:
                                             none,0,0
                Conversion coefficient data (maximum 5 items)
                 ** NTR,EXP,DEXP,L1,H1(,L2,H2)
                  where ** is any unique combination of symbols (e.g., CC,
                  AK)
                        NTR   The number of the transition (1 or 2)
                        EXP   Experimental value
                        DEXP  Uncertainty
                        L1    Theoretical value for the lower multipole
                              (SHELL1)
                        H1    Theoretical value for the higher multipole
                              (SHELL1)
                              For ratios SHELL1/SHELL2:
                        L2    Theoretical value for the lower multipole
                              (SHELL1)
                        H2    Theoretical value for the higher multipole
                              (SHELL2)
 
                Sample input data set: DELTA.DAT
 
          Output file (Short output marked with an asterisk (*)):
                For each spin combination (each GO card):
                  * Option and data cards read
                  * Header
                  * Data
                    Header
                    CHI**2 and best theoretical values of data (step in
                      DELTA1)
                  * Best DELTA1
                    Header
                  * Plot of CHI**2 versus ATAN(DELTA1)
                    Header
                    CHI**2 and best theoretical values of data (step in
                      DELTA2)
                  * Best DELTA2
                  * Plot of CHI**2 versus ATAN(DELTA2)
                  * 'END OF ANALYSIS FOR THIS SPIN COMBINATION'
 
                Optionally a dump of common block variables can be
                obtained.
 
                Sample output: DELTA.RPT
 
 
                                       3
 
                                     DELTA
                         Version 1.01 [April 15, 1993]
 
 
          Terminal dialog:  The user will be requested to supply the  input
                file name and the output file name.
 
          Compilation and loading instructions:  No special instructions
 
          Memory and time requirements:
                Norsk Data ND-500: 58 kB. 8 sec. for one spin sequence and
                both deltas varied
                386DX/25 with 387: 80226 bytes. 13 sec. for sample input.
 
          Additional documentation:  DELTA - A COMPUTER PROGRAM TO  ANALYZE
                GAMMA-GAMMA   CORRELATIONS  FROM  UNALIGNED  STATES.   L.P.
                Ekstrom.  Nuclear  Physics  LUNFD6/(NFFR-3048)  1-27  (Lund
                University.  1983).
 
                                   Version History
                           L.P. Ekstrom, Lund
          1                I/O unit number changed (YS)
          1.01  15-Apr-93  Delinted using FLINT 2.83
                           Explicitely typed all variables and functions
                           Floating overflow in SETFAC corrected and
                             routines using factorials adjusted to handle
                             change in data storage
                           Corrected CLOSE statement on error in OPENFI
                           Fixed output conversion problem
                           (TWB)
 
                                     Disclaimer
 
               Neither  the  Brookhaven  Science  Associates,  nor  the  US
          Department  of  Energy  make  any  warranty  or  assume any legal
          responsibility for the results produced by the program.
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
                                       4
