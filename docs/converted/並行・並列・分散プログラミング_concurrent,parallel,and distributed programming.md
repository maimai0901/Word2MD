# $BJB9T!&JBNs!&J,;6(B$B%W%m%0%i%\_%s%0(B/concurrent,parallel,and distributed programming

```
$BJB9T(B$B%7%9%F%`(B

                               $B%7%9%F%`(B$B>pJs7O(B/$B>pJs9)3X0h(B,
			       $B%7%9%F%`(B$B>pJs9)3X8&5f72(B/$B>pJsM}9)3X0L(B$B%W%m%0%i%`(B
			       $B%7%9%F%`(B$B>pJs9)3X8&5f2J(B/$B%3%s%T%e!<%?%5%$%(%s%9(B$B@l96(B
                               [$B?7>k(B $BLw(B](http://www.cs.tsukuba.ac.jp/~yas/)
                               <yas@cs.tsukuba.ac.jp>

```

$B$3$N(B$B%Z!<%8(B$B$O!"
 `<http://www.cs.tsukuba.ac.jp/~yas/cs/csys-2023/2023-04-14>`
$B$"$k$$$O!"$B%Z!<%8(B$B$+$i
 `<http://www.cs.tsukuba.ac.jp/~yas/cs/>`
 `<http://www.cs.tsukuba.ac.jp/~yas/>`

## $B"#:#F|$N=EMW$JOC(B

$BMQ8l$N0U5A(B

* $BJB9T(B concurrent
* $BJBNs(B parallel
* $BJ,;6(B distributed

$BNr;K(B history

* $B#O#S$HC10l(B$B%W%m%0%i%\_%s%0(B$B!?(B$B%^%k%A%W%m%0%i%\_%s%0(B OS and sequential programming/ multiprogramming
* $BF14|DL?.(B$B%W%j%\_%F%#%V(B$B!#(B$B%m%C%/(B$B!"(B$B%;%^%U%)(B$B!"(B$B%b%K%?(B$B!"(B$B%i%s%G%V(B$B!#(B
  Synchronization primitives. locks, semaphores, monitors, rendezvous.
* $B%W%m%0%i%\_%s%0(B$B8@8l$K$h$k;Y1g!#(B
  Programming language support.
* SMP $B$H(B$B%9%l%C%I(B$B!#(B
  SMP and threads.

$B%O!<%I%&%'%"(B

* UMA (Uniform Memory Access), SMP (Symmetric Multiprocessor)
* NUMA (Non-uniform Memory Access)
* NORMA (No-Remote Memory Access)

$B3d$j9~$\_$HJB9T(B$B%W%m%0%i%\_%s%0(B
Interrupts and concurrent programming

* $B3d$j9~$\_6X;\_$K$h$kAj8\_GS=|!#(B
  mutual exclusion by disabusing interrupts

## $B"#JB9T!&JBNs!&J,;6(B$B%W%m%0%i%\_%s%0(B(concurrent, parallel, and distributed programming)

### $B"!C`$B%W%m%0%i%\_%s%0(B$B$HJB9T(B$B%W%m%0%i%\_%s%0(B(sequential and concurrent programming)

$BC`: $B#1EY$K#1$D$N $BJB9T(B concurrent : $B#1EY$KJ#?t$N

```
main()
{
	printf("hello, world!\n");$B!!(B
}

```

$BC`$B%W%m%0%i%`(B$B$G$O!"(B1$BEY$K(B1$B$D$N

$BJ#?t$N$B%W%m%;%9(B(process)$B!W$d!V(B$B%9%l%C%I(B
(thread)$B!W!#(B

![$B=D<4;~4V!](./$BJB9T!&JBNs!&J,;6%W%m%0%i%_%s%0(B_concurrent,parallel,and distributed programming_files/seq-con-threads-coordinate.png)

**$B?^(B? $BC`$B%W%m%0%i%`(B$B$HJB9T(B$B%W%m%0%i%`(B$B$NF0:n(B($B;~4V$H6u4V$N4QE@$+$i(B)**

### $B"!JBNs=hM}$HJ,;6=hM}$NL\E\*(B (Objectives of parallel processing and distributed processing)

$BJBNs(B parallel
:   $B#1$D$NLdBj$r!JC`

    $BJ,;6(B distributed (A)
    :   **$BN%$l$F$$$F$b?4$O#1$D(B** sharing one heart between two separate lovers

    $BJ,;6(B distributed (B)
    :   1$BBf$N(B$B%3%s%T%e!<%?(B$B$N(B$B%a%b%j(B$B$K>h$i$J$$(B$B%G!<%?(B$B$r07$$$?$$!#(B
        (2$B

$B$3$N

$B!VJ,;6(B distributed (A)$B!W$O!"C`

* $B%U%)!<%k%H%H%l%i%s%9(B fault torrance$B!#(B
  $BMWAG$N0lIt$,8N>c$7$F$$$F$b(B(partial failure)$B$G$bF0$-B3$1$k!#(B
* $B9=@.MWAG$NA2?JE\*$JCV49(B incremental replacement of components$B!#(B
  $B2u$l$?ItIJ$r* $B?M

### $B"!JB9T(B$B%W%m%0%i%\_%s%0(B$B!JJBNs!"J,;6!"$=$NB>!K$N6&DL$NOC(B

* ($B%W%m%;%C%5(B$B$,J#?t(B) (multiple processors)
* $B%W%m%;%9(B$B$,J#?t(B multiple processes
* $B%W%m%;%9(B$B4V$N6(D4(B(coordination)$B$,I,MW!#F14|(B(synchronization)$B!"DL?.(B(communication)$B!#(B
* $B;q8;3d$jEv$F(B(resource allocation)$B!"(B$B%9%1%8%e!<%j%s%0(B(scheduling )$B$,=EMW!#(B

$BC10l(B$B%W%m%;%C%5(B$B$G$NJB9T(B$B%W%m%0%i%\_%s%0(B$B$b$"$k!#8e=R!#(B
concurrent programming in a single processor.

### $B"!JB9T(B$B%W%m%0%i%\_%s%0(B$B$GI,MW$J8@8l(B

$B#2$D$N8@8l$,I,MW(B

$B7W;;8@8l(B computational languages
:   $B8D!9$N3hF0$r5-=R(B

    * C
    * Fortran

$B6(D48@8l(B coordination languages
:   $BE}0l$5$l$?(B$B%W%m%0%i%`(B$B$KAH$\_N)$F$k$?$a$N!V8R(B(glue)$B!W(B

    * Linda
    * ($BF14|!&DL?.%i%$%V%i%j(B)

Java $B$J$I!"#1$D$N8@8l$G7W;;$H6(D4$,=q$1$k$b$N$b$"$k!#(B

## $B"#Nr;K(B history

$BNr;KE\*$K=EMW$J=PMh;v$HJB9T(B$B%W%m%0%i%\_%s%0(B$B$r3X$V0U5A!#(B

$B9V5A$N:G8e$K$O!"$3$3$G8=$l$k(B$B%-!<%o!<%I(B$B$rM}2r$G$-$k$3$H$rL\I8$K$9$k!J:#(B
$BF|$NCJ3,$G$OM}2r$G$-$J$$$b$N$,$"$C$F$b$h$$!K!#(B

### $B"!C`$B%W%m%0%i%\_%s%0(B$B$NH/L@(B invention of sequential programming

$B%O!<%I%&%'%"(B$B$O!"K\

$B%W%m%0%i%`%+%&%s%?(B$B$NH/L@!#(B$B%W%m%0%i%`(B$BFbB"J}<0!#(B
$B%N%$%^%s(B$B7?(B$B%3%s%T%e!<%?(B$B!#(B

$BC`o$KFC

* $BNr;KE\*$JET9g!#(B$B%O!<%I%&%'%"(B$B$,9b2A$@$C$?!#(B
  $BJ#?t(B$B%3%s%T%e!<%?(B$B$r;H$&$N$OlTBt$9$.$k!#(B
* **$BC`$B%W%m%0%i%`(B$B$N=q$-$d$9$5(B**$B!#@)8B$r$D$1$?J}$,$o$+$j$d$9$$!#(B
  $B3XIt(B1$BG/@8$G$b(B$B%W%m%0%i%`(B$B$,$+$1$k!#(B

$BEv=i$N(B$B%3%s%T%e!<%?(B$B$K!"#O#S$O$J$$!#(B

### $B"!(B$B%^%k%A%W%m%0%i%\_%s%0(B multiprogramming

$B#1Bf$N(B$B%3%s%T%e!<%?(B$B$N(B$B%a%b%j(B$B$K!"F1;~$KJ#?t$N(B$B%W%m%0%i%`(B$B$r(B$B%m!<%I(B$B$7$F@Z$jBX(B
$B$($J$,$iF0:n$5$;$k!#(B

$B%O!<%I%&%'%"(B$B$O!"9b$$!#(B

$B9b$$#C#P#U$rM-8z$K3hMQ$7$?$$!#(B

$B%P%C%A(B$B=hM}$NCB@8!#F~=PNO$H#C#P#U=hM}$r!VJBNs!WF0:n$5$;$k!#(B

![$B#3$D$N%8%g%V$NC`<!=hM}!#3F%8%g%V$O!](./$BJB9T!&JBNs!&J,;6%W%m%0%i%_%s%0(B_concurrent,parallel,and distributed programming_files/batch-input-proc-output-seq.svg)

**$B?^(B? 3$B$D$N(B$B%8%g%V(B$B$NC`**
![$B%8%g%V$,#3$D!](./$BJB9T!&JBNs!&J,;6%W%m%0%i%_%s%0(B_concurrent,parallel,and distributed programming_files/batch-input-proc-output.svg)

**$B?^(B? $B%P%C%A(B$B=hM}$K$\*$1$k(B CPU $B$HF~=PNOAuCV$NJBNsF0:n(B (parallel processing of CPU and I/O in batch processeing)**

$B%W%m%;%9(B$B$N35G0$N3NN)!#(B$B%W%m%;%9(B$B$H(B$B%W%m%0%i%`(B$B$NJ,N%!#(B
$B0lHL$N(B$B%W%m%0%i%\_%s%0(B$B$O!"C`

$B#O#S$@$1JB9T(B$B%W%m%0%i%\_%s%0(B

* $BFq$7$$JB9T(B$B%W%m%0%i%\_%s%0(B$B$r#O#S$KJD$89~$a$F!";D$j$O3Z$r$9$k!#(B
* $B#O#S$O$,$s$P$C$F:n$k(B

$B:#$G$b#O#S$N652J=q$K$O!"(B$B%;%^%U%)(B$B$d(B$B%G%C%I%m%C%/(B$B$NOC$,=P$F$$$k!#(B

Concurrent Pascal, Solo$B!#(B

$B#O#S$N

### $B"!C10l(B$B%W%m%;%C%5(B(a single processor)

$BC10l(B$B%W%m%;%C%5(B$B!#(B
$B5;=QE\*$K3NN)$7$F$$$k!#(B
![CPU$B!](./$BJB9T!&JBNs!&J,;6%W%m%0%i%_%s%0(B_concurrent,parallel,and distributed programming_files/single-processor.svg)

**$B?^(B? $BC10l(B$B%W%m%;%C%5(B (a single processor system)**

### $B"!(BUnix fork-exit-wait

$B%f!<%6%l%Y%k(B$B$NL?Na$NNc(B

* fork()
* exit()
* wait()

fork join model

### $B"!(BTSS (Time sharing system)

Time sharing system$B!#(B

$B#1Bf$NCf1{$NBg7?(B$B%3%s%T%e!<%?(B(mainframe)$B$K!"J#?t$N!V!JJ8;z!KC

$BC

TSS $B$GJ#?t$N(B$B%"%W%j%1!<%7%g%s(B$B$rF1;~$KAv$i$;$k!#(B
CPU $B$,5.=E$J;~Be!#(BCPU $B$rM7$P$;$J$$!#(B

![$B%a%$%s%U%l!<%`#1Bf!](./$BJB9T!&JBNs!&J,;6%W%m%0%i%_%s%0(B_concurrent,parallel,and distributed programming_files/mainframe-terminals.png)

**$B?^(B? $B%a%$%s%U%l!<%`(B$B$HC**

### $B"!(BVirtual Machine

$B#1Bf$N(B$B%a%$%s%U%l!<%`(B$B$K!"F1;~$KJ#?t$N#O#S$rAv$i$;$k$N$,;O$j!#(B
TSS $B$N

$B:G6a$O!"(B
$B%3%s%T%e!<%?(B$B$N9bB.2=$G!"@-G=$,M>$C$F$-$?!#$b$H$b$H(B$B%O!<%I%&%'%"(B$B#nBf$G$d$C(B
$B$F$$$?;E;v$r!"(B$B%O!<%I%&%'%"(B$B$H$7$F$O#1Bf$K=8Ls$9$k!#JBNs=hM}$N5U!#(B

![$B?^(B? $B%5!<%P#3Bf!](./$BJB9T!&JBNs!&J,;6%W%m%0%i%_%s%0(B_concurrent,parallel,and distributed programming_files/virtual-machine-server-consolidation-before.png)$l#2$D(B">

**$B?^(B? $B2>A[7W;;5!$K$h$k(B$B%5!<%P(B$B$N=8Ls(B($B=8LsA0(B) (before server consolidation by virtual machines)**
![$B?^(B? $B%O!<%I%&%'%](./$BJB9T!&JBNs!&J,;6%W%m%0%i%_%s%0(B_concurrent,parallel,and distributed programming_files/virtual-machine-server-consolidation-after.png)$l#2$D(B">

**$B?^(B? $B2>A[7W;;5!$K$h$k(B$B%5!<%P(B$B$N=8Ls(B($B=8Ls8e(B) (after server consolidation by virtual machines)**

1999$BG/(BVMware Workstation $B0J9\_!"(B$B%Q%=%3%s(B$BMQ$N(B VM $B$b9-$/;H$o$l$k!#(B

### $B"!(B$B%G!<%?%Y!<%9(B(database)

$B%W%m%0%i%`(B$B$H(B$B%G!<%?(B$B$rJ,N%!#(B$B%G!<%?(B$B$rJ#?t$N(B$B%W%m%0%i%`(B$B$G6&M-(B(share)$B!#(B
$B%G!<%?(B$B$rCf?4$K9M$($k!#(B
$B%G!<%?(B$B$K(B integrity $B$r;}$?$;$k!#(B
integrity $B$rK~$?$7$?(B$B%G!<%?(B$B$@$1$r!"$-$A$s$H(B
$B1JB3E\*(B(persistent)$B$KJ]B8$9$k!#(B

### $B"!(B$B%H%i%s%6%/%7%g%s(B(transaction)

$BJ#?t$N(B$B%G!<%?%Y!<%9(B$B$X$NLd$$9g$o$;!J8!:w!"99?7!K$r!"$G$-$k$@$1!VJB9T(B
(concurrent)$B!W$K

$B:G=\*7k2L$O!"#1$D$R$H$DC`

### $B"!(BLocal Area Network$B$H(Bworkstation

Sun Workstation$B!#(B

$B;q8;$r6&M-$7$?$$!#(B$B%W%j%s%?(B$B!#(B$B%G%#%9%/(B$B!#(B

$B%G%#%9%/%l%9!&%o!<%/%9%F!<%7%g%s(B$B!#(B

Socket API$B!"(BX Window$B!"(B
NFS, NIS, RPC $B=P8=!#(B

### $B"!(BSocket API

$B$b$H$b$H(B Unix 4.2 BSD $BMQ!#(B
socket(), listen(), accept(), connect(), send(), recv(), select()$B!#(B

$BJ#?t$NDL?.(B$B%W%m%H%3%k(B(TCP/IP$B0J30$b(B)$B$r07$($k!#(B

### $B"!(BX Window

X Window$B!#(B$B%&%$%s%I%&(B$B$N(B$B%W%m%0%i%\_%s%0(B$B$O!"K\$B%/%i%$%"%s%H!&%5!<%P!&%b%G%k(B(client server model)$B$K4p$E$/!#(B
$B$?$@$7!"8e$K!"(B$B%b%G%k(B$B$rJQ99$7$?!#(B
$B%5!<%P(B$B$+$i(B$B%/%i%$%"%s%H(B$B$X$N(B$B%$%Y%s%H(B(events)$B$NAw?.$rIU$1$?!#(B
$B%j%9%J!&%Q%?%s(B(listener pattern)$B$X$HH/E8!#(B

### $B"!(BRemote Procedure Call(RPC)

$B1s3V$B%W%m%;%9(B$B4VDL?.(B(interprocess communication)$B$@$,!"0l8+!"(B
$B

RPC $B$O!"(BNFS (Network File System) $B$N$B%5!<%P(B$B!"(B
$BA43X7W;;5!(B icho01, icho02, kiri $B$G!"(B
$B$I$N(B$B%3%s%T%e!<%?(B$B$r;H$C$F$b!"<+J,$N(B$B%[!<%`%G%#%l%/%H(B$B$,8+$($k$N$O!"(BNFS $B$r(B
$B;H$C$F$$$k!#(B

NFS $B$N$?$a$K(B UID (user id) $B$H(B$B%Q%9%o!<%I(B$B$r6&M-$9$k$?$a$K;H$o$l$?$N$,(B
NIS (Network Information System)$B!#(B

### $B"!JB9T(B$B%W%m%0%i%\_%s%0(B$B8@8l(B

* $B%Z%H%j%M%C%H(B Petri Net
* CSP (Communicating Sequential Processes)
* Actors
* Concurrent Pascal, Distributed Processes($B8@8l$NL>A0(B)
* Ada
* PLITS, Synchronizing Resources, Cell
* Argus

### $B"!(BAda

Ada$B!#(B$B%"%a%j%+(B$B9qKI>J(B(US DoD, Department of Defence)
$B$G;EMM$r7h$a$?AH$\_9~$\_(B$B%7%9%F%`(B(embedded systems)$BMQ$N(B
$B%W%m%0%i%\_%s%0(B$B8@8l!#(B

* $B;EMM(B(specification)$B!J(B$B%$%s%?%U%'!<%9(B(interface)$B!K$H* $B%W%m%;%9(B$B@8@.(B
  * $B%i%s%G%V(B(rendezvous)$B$K$h$k(B$B%W%m%;%9(B$B4VDL?.(B

### $B"!(B$B%W%m%0%i%\_%s%0(B$B8@8l$,Ds6!$9$k35G0(B

$BJB9T$B%,!<%I(B$BIU$-(B$B%3%^%s%I(B(guarded commands)$B!#(B

$BE/3XCHq$B%P%C%U%!(B$BLdBj(B(bounded buffers)$B!#(B$B%G%C%I(B
$B%m%C%/(B(deadlock)$B!#(B

$B=i4|$N$B%3%k!<%A%s(B(coroutine)$B!#(B

### $B"!(B$B%\*%V%8%'%/%H(B$B;X8~(B$B%W%m%0%i%\_%s%0(B(object oriented programming)

$B%W%m%0%i%`(B$B$r(B$B%\*%V%8%'%/%H(B(objects)$B$N=89g$G=q$/!#(B
$B%\*%V%8%'%/%H(B$B$O!"?M4V$N$h$&$K!"<+N'(B(autonomous, autonomic)$B$7$F$$$k!#(B
$B%\*%V%8%'%/%H(B$B$NFbIt$N(B$B%G!<%?(B$B$O30$+$i?($l$J$$!#(B$B%G!<%?%Y!<%9(B$B$N5U!#(B
$B%\*%V%8%'%/%H(B$B$NFbIt$r(B$B%"%/%;%9(B$B$9$k$K$O!"(B$B%a%C%;!<%8(B(message)$B$rAw$k$7$+$J$$!#(B

$B%\*%V%8%'%/%H(B$B;X8~(B$B%W%m%0%i%\_%s%0(B$B$O!"K\$B%W%m%0%i%\_%s%0(B$B!#(B
$B

obj1.method1();

Smalltalk 80

$B%\*%V%8%'%/%H(B$B;X8~(B$B%G!<%?%Y!<%9(B(object-oriented databases)$B$NL7=b!#(B

### $B"!(BORB

Object Request Broker$B!#J#?t$N8@8l$r7R$.$?$$!#(B
$B%\*%V%8%'%/%H(B$B;X8~$,F~$C$?(B RPC $B!#(B

### $B"!DL?.(B$B%i%$%V%i%j(B(Communication Library)

* PVM, Parallel Virtual Machine
* MPI, Message Passing Interface

### $B"!(B$B%Q%=%3%s(B(Personal Computers)

$BHf3SE\*?7$7$$!#(B

### $B"!(BCP/M (Control Program for Microcomputers)

$B%Q%=%3%s(B$BMQ$N!J(B$B%U%m%C%T(B$B!&!K(B$B%G%#%9%/(B$B#O#S!J(B(floppy)Disk Operating System$B!K!#(B
$B0lEY$K#1$D$@$1(B$B%W%m%0%i%`(B$B$,F0$/!#(B
$B%-!<%\!<%I(B$BF~=PNO!"(B$B%U%m%C%T!&%G%#%9%/(B$B$N#D#M#AE>Aw40N;$K$O3d$j9~$\_$r;H$&!#(B

### $B"!(BMacintosh Multi-finder

$B!V(B$B%Q%=%3%s(B$B$G!W!"0lEY$KJ#?t$N(B$B%W%m%0%i%`(B$B$r@Z$jBX$($J$,$i;H$($k!#(B

### $B"!(BMS-DOS

CP/M $B$K!"(BUnix $BE\*$J5!G=$rF~$l$?!#(B

1. $B3,AX2=(B$B%G%#%l%/%H%j(B(hierarchical directories)$B!#(Bmkdir, chdir
2. $B;R(B$B%W%m%;%9(B$B$O:n$l$k(B(child processes)$B!#!J<+J,$O;\_$^$k!#!K(B

### $B"!(BMS Windows

$B!V(B$B%Q%=%3%s(B$B$G!W!"J#?t$N(B$B%W%m%0%i%`(B$B$rF1;~$KF0$+$7$F$b!"$&$^$/F0$/$h$&$K$J$C(B
$B$?!#(B

MS Windows 95 $B$O!"FbItE\*$K$O!"(BCOM/OLE $B$H8F$P$l$k(B ORB $B$N8G$^$j$G:n$i$l(B
$B$F$$$k!#(B

$B%Q%=%3%s(B$B$G$O!"J]8n$N35G0$,4uGv!#(B

### $B"!(B$B%^%k%A%W%m%;%C%5(B(a multi processor)

[$BC10l(B$B%W%m%;%C%5(B$B$G(B](https://www.cs.tsukuba.ac.jp/~yas/cs/csys-2023/2023-04-14/index.html#single-processor-computer) CPU $B$rA}$d$9!#(B
![CPUx3$B8D!](./$BJB9T!&JBNs!&J,;6%W%m%0%i%_%s%0(B_concurrent,parallel,and distributed programming_files/multi-processor.svg)

**$B?^(B? $B%^%k%A%W%m%;%C%5(B (a mult-processor)**

### $B"!(BIntel Hyperthreading

CPU$B$N(B$B%W%m%0%i%`!&%+%&%s%?(B$B2s$j$@$1A}$d$7$?$b$N!#(B

### $B"!(BMulti-core

$B#1$D$N(B$B%A%C%W(B$B$K!"J#?t$N(B CPU $B$r:\$;$k!#(B

$B:#$NCJ3,$G$O!"C1$K!"(BCPU 2 $B8D$"$k$b$N$r(B 1 $B8D$K$^$H$a$?$h$&$J$b$N!#(B
$B@N$N(B SMP $B!]!d(B UMA $B$N:F8=!#(B$B%3%"(B$B?t!"(B$B%A%C%W(B$B?t$,A}$($k$K=>$$!"(B
$BIT6Q

### $B"!(BInternet

TCP/IP$B$N#4AX(B$B%b%G%k(B$B!#(B
OSI $B$N#7AX(B$B%b%G%k(B(seven layer model)$B$h$j8E$$!#(B

$B%/%i%$%"%s%H!&%5!<%P!&%b%G%k(B(client server model)$B!#(B

inetd (Internet daemon)$B!#(B

### $B"!(BUUCP (Unix-to-Unix Copy)

$BIOK3?M$N(B Internet$B!#(Bpoor man's Internet

$B:#$NMQ8l$@$H(B$B%b%G%`(B(modem)$B$K$h$k(B$B%@%$%d%k%"%C%W(B(dial up)$B@\B3$rMQ$$$?(B
peer-to-peer (P2P) $B7?$N(B$B%U%!%$%k(B$BE>Aw(B(file transfer)$B!#(B
$BEE;R(B$B%a!<%k(B(email)$B$H(B$B%M%C%H%K%e!<%9(B(netnews, Usenet)$B$N5-;v$r1?$V!#(B

$B%K%e!<%9%7%9%F%`(B(news system)$B$N;EAH$\_$O!"J,;6(B$B%7%9%F%`(B$B$NM%$l$?Nc$K$J$C$F$$$k!#(B

### $B"!(Bftp

$B%=%U%H(B$B$NG[I[$HO@J8Ej9F!#(B
anonymous ftp$B!#(Barchie.
$BLkCf$KAv$i$;$k$N$,Ni57!#(B

### $B"!(BWorld Wide Web

$BJ8;z$?$1$G$J$/!"3($,=P$k!#(B$B%X%k%Q!<(B$B$G2;$b=P$k!#(B

$B%/%i%$%"%s%H!&%5!<%P!&%b%G%k(B(client server model)$B!#(B
$B%P%C%A(B$B=hM}Iw(B(batch processing like)$B!#(B

### $B"!(BCGI

Common Gateway Interface$B!#(B

$B:G6a$G$O!"B?$/$N?M$,!"(BCGI $B$G$O$8$a$FJB9T(B$B%W%m%0%i%\_%s%0(B$B$K=P2q$&!#(B

$B%m%C%/(B$B$7$J$$$H(B$B%@%a(B$B!#(B$B%G%C%I%m%C%/(B$B$,5/$jF@$k!#(B

### $B"!(BJava Applet

Web$B%V%i%&%6(B$B$G!"(B$B%"%K%a!<%7%g%s(B$B$r9T$&$?$a$KEP>l!#(B

### $B"!(BJava Servlet

$B=E$?$$(B fork() $B$rHr$1$k!#(B

### $B"!(BXML Web Service

ORB $B$N

HTML$B!#(BXML$B!#(BHTTP$B!#(BSOAP$B!#(B

### $B"!(BRepresentational state transfer (REST)

XML Web Service $B$N

### $B"!(BP2P

Peer-to-peer $B!#(B

$B%/%i%$%"%s%H!&%5!<%P(B$B$N0U5A$,Bg;v!#(B
$B%/%i%$%"%s%H!&%5!<%P(B$B$,8=$l$kA0$N>u67$KLa$C$F$O$$$1$J$$!#(B

Single Point of Failure $B$rHr$1$k$H$$$&9M$(J}$O$h$$!#(B

### $B"!(B$B%/%i%&%I!&%3%s%T%e!<%F%#%s%0(B(cloud computing)

* $B%G!<%?%;%s%?!<(B(data centers)$B$K;q8;$r=8Cf$5$;$k(B
* $BJ#?t4k6H$G;q8;$r6&M-$9$k!#(B

[$B%a%$%s%U%l!<%`(B$B$K$h$k(BTSS](https://www.cs.tsukuba.ac.jp/~yas/cs/csys-2023/2023-04-14/index.html#tss)$B$N:FMh$H$b8@$($k!#(B

## $B"#(B$B%O!<%I%&%'%"(B / hardware

### $B"!(B$B%7%s%0%k%W%m%;%C%5(B$B$H=8Cf7?(B$B%7%9%F%`(B / single processors and centralized systems

$B%7%s%0%k%W%m%;%C%5(B$B$O!"#1Bf$N(B$B%3%s%T%e!<%?(B$B$K(B$B%W%m%;%C%5(B$B$,(B CPU $B$,(B 1 $B$D!"%a(B
$B%b%j(B$B$b(B 1$B$D!#(B

$B%M%C%H%o!<%/(B$B$G@\B3$5$l$?J#?t$N(B$B%3%s%T%e!<%?(B(multiple computers that are
connected with a network)$B$+$i9=@.$5$l$kJ,;6(B$B%7%9%F%`(B(distributed
systems)$B$HBPHf$9$k;~$K$O!"=8Cf7?(B$B%7%9%F%`(B(centralized systems))$B$H8F$P$l(B
$B$k!#(B

$B5;=QE\*$K3NN)$7$F$$$k!#(B

![CPU$B!](./$BJB9T!&JBNs!&J,;6%W%m%0%i%_%s%0(B_concurrent,parallel,and distributed programming_files/single-processor.svg)

**$B?^(B? $BC10l(B$B%W%m%;%C%5(B (a single processor system)**

### $B"!JBNs(B$B%3%s%T%e!<%?(B(parallel computers)

Flynn $B$NJ,N`(B (Flynn's taxonomy)

* SISD, Single Instruction, Single Data
* SIMD, Single Instruction, Multiple Data
* MISD, Multiple Instruction, Single Data
* MIMD, Multiple Instruction, Multiple Data

MIMD $B$NJ,N`(B

* $B6&M-(B$B%a%b%j(B$B$,$"$k(B(with shared memory)
* $B6&M-(B$B%a%b%j(B$B$,$J$$(B(without shared memory)

Mach$B%7%9%F%`(B$B$G$NJ,N`(B ( Mach operating system kernel, Mach microkernel )

* $B6&M-(B$B%a%b%j(B$B$,$"$k(B(with shared memory)
  + $B%"%/%;%9$,6Q+ $B%"%/%;%9$,IT6Q
* $B6&M-(B$B%a%b%j(B$B$,$J$$(B: NORMA (No-Remote Memory Access)$B!#(B

### $B"!6&M-(B$B%a%b%j(B$B7?(B$B%^%k%A%W%m%;%C%5(B$B!"(BSMP (Shared memory multiprocessor)

![(CPU+Cache)*n+$B%a(B
$B%b%j(B](./$BJB9T!&JBNs!&J,;6%W%m%0%i%_%s%0(B_concurrent,parallel,and distributed programming_files/shared-memory-multiprocesor.png)

**$B?^(B? $B6&M-(B$B%a%b%j(B$B7?(B$B%^%k%A%W%m%;%C%5(B($B%P%9(B$B6&M-(B) (Shared memory multiprocessor (with a shared bus))**

* Symmetric multiprocessor (SMP)$B$H$b8@$&!#(B$B%a%b%j(B$B$X$N(B$B%"%/%;%9(B$B;~4V$,$I$N>l=j$bBP>NE\*$G6Q* $BJ,;6(B$B%7%9%F%`(B$B$K$OJ,N`$7$J$$$N$,IaDL!#(B
    $B=8Cf(B$B%7%9%F%`(B$B$N(B$B%W%m%0%i%`(B$B$,$=$N$^$^F0:n$9$k$N$G!#(B
  * $B%-%c%C%7%e(B$B$N?FOB@-(B(cache affinity)$B$^$G9M$($k$HJ,;6E\*$J5;=Q$,$$$k!#(B
    $B%a%b%j(B$B$N@09g@-(B(memory consistency)$B$^$G9M$($k$H!"K\Ev$O$+$J$jFq$7$$!#(B
  * $B%^%k%A%3%"(BCPU (multi-core CPU)$B$O!"C1BN$G(BSMP$BJ,N`$5$l$k!#Nr;KE\*$K$O8E$$!#(B

### $B"!(B$B%/%m%9%P!<%9%$%C%A(B(crossbar switch)

![n*CPU-n*Memory](./$BJB9T!&JBNs!&J,;6%W%m%0%i%_%s%0(B_concurrent,parallel,and distributed programming_files/crossbar-switch-multiprocesor.png)

**$B?^(B? $B6&M-(B$B%a%b%j(B$B7?(B$B%^%k%A%W%m%;%C%5(B($B%/%m%9%P!<%9%$%C%A(B) (shared memory multiprocessor with a crossbar switch)**
$BJ#?t$N(BCPU$B$,JL$N(B$B%a%b%j(B$B$KF1;~$K(B$B%"%/%;%9(B$B$G$-$k!#(B
$BF1$8(B$B%a%b%j(B$B$J$i(B$B%P%9(B$B$HF1MM$K>WFM$9$k!#(B

### $B"!Hs6Q$B%a%b%j(B$B7?(B$B%^%k%A%W%m%;%C%5(B(shared memory multiprocessor with non-uniform memory access)

![CPU$B!](./$BJB9T!&JBNs!&J,;6%W%m%0%i%_%s%0(B_concurrent,parallel,and distributed programming_files/non-uniform-memory-access.png)

**$B?^(B? $BHs6Q$B%a%b%j(B$B7?(B$B%^%k%A%W%m%;%C%5(B (shared memory multiprocessor with non-uniform memory access)**
$BAj8\_7k9g(B$B%M%C%H%o!<%/(B$B$G!"1s3V$N(B$B%a%b%j(B$B$r(B CPU $B$+$iD>@\(B$B%"%I%l%9(B$B$G(B$B%"%/%;%9(B
$B$G$-$k!#$?$@$7!"B.EY$O(B 100 $BG\$/$i$$CY$$!#(B

### $B"!(BLAN$B$K@\B3$5$l$?(B$B%3%s%T%e!<%?(B$B72(B(multiple computers connected to a LAN)

![PC*3--hub](./$BJB9T!&JBNs!&J,;6%W%m%0%i%_%s%0(B_concurrent,parallel,and distributed programming_files/pc-swiching-hub.png)

**$B?^(B? LAN$B$K@\B3$5$l$?(BPC**
[NORMA](https://www.cs.tsukuba.ac.jp/~yas/cs/csys-2023/2023-04-14/index.html#norma)$B$N0l$B"!(B$B%H!<%i%9(B Torus
![3x4 2d torus](./$BJB9T!&JBNs!&J,;6%W%m%0%i%_%s%0(B_concurrent,parallel,and distributed programming_files/torus-2d.png)

**$B?^(B? 2$B$B%H!<%i%9(B**
$B3J;R>u$@$,!"C<$,H?BPB&$H$D$J$,$C$F$$$k!#(B
$B@$$NCf!"(B3$B$B%H!<%i%9(B$B$NG[@~$O4JC1!#(B

3$Be$N(B$B%H!<%i%9(B$B$b2DG=$@$,!"G[@~$,BgJQ$K$J$k!#(B

### $B"!(B$B%O%$%Q!<%-%e!<%V(B Hypercube

![$B%O%$%Q!<%-%e!<%V(B(1$B<!85(B-4$B<!85(B)](./$BJB9T!&JBNs!&J,;6%W%m%0%i%_%s%0(B_concurrent,parallel,and distributed programming_files/hypercube.svg)

**$B?^(B? $B%O%$%Q!<%-%e!<%V(B(1$B**
2$B$B%H!<%i%9(B$B$h$j$b!"(B$B%N!<%I(B$B4V$N(B$B%[%C%W(B$B?t$,>/$J$$!#(B

$BG[@~$,BgJQ$K$J$k!#(B

## $B"#3d$j9~$\_(B(interrupt)

$B%^%k%A%W%m%;%C%5$G$O$J$$!"C10l(BCPU$B$N%7%9%F%`$G!"8zN(E\*$KJB9T%W%m%0%i%`(B
$B$r5-=R$9$k$?$a$N;EAH$\_!#(B
CPU $B$H<~JUAuCV$NJBNs=hM}$K;H$&!#(B
$B%O!<%I%&%'%"$ND>@\E\*$J%5%]!<%H$,$"$k!#(B

$B3d$j9~$\_$N%W%m%0%i%\_%s%0$O!"Hs>o$KFq$7$$!#%G%P%C%,$,;H$($J$$!#(B
printf() $B$b$D$+$($J$$!#(B

$B$?$@$7!"JB9T@-$N5-=R$K$D$$$F$O!"%9%l%C%I$N%G%C%I%m%C%/$h$j$O!">l9g$K$h$C(B
$B$F$O4JC1$+$b$7$l$J$$!#(B

$B$b$H$b$H%9%l%C%I$N%W%m%0%i%`$r3d$j9~$\_$N%W%m%0%i%`$K=q$-49$($k$N$O(B
$BFq$7$$!#(B

### $B"!<~JUAuCV(B(peripheral devices)

$BF~=PNOAuCV(B($B%G%P%$%9(B)$B!"%G%P%$%9(B(device)
$B$H$O!"%3%s%T%e!<%?$NH"$NCf$KFbB"$5$l$F$$$k%O!<%I%&%'%"$NItIJ$d%1!<%V%k(B
$B$G30$G@\B3$9$kItIJ!#(B
$BIaDL$O!"(BCPU $B$H%a%b%j0J30$N$3$H$r;X$9!#(B
$B<~JUAuCV(B(peripheral device)$B!"(B
$BF~=PNOAuCV(B(IO device)$B$H$b8F$P$l$k!#(B

* $B%O!<%I%G%#%9%/(B(hard disks)
* $B%-!<%\!<%I(B(keyboard)
* $B%^%&%9(B(mouse)
* $B%0%i%U%#%/%9!&%+!<%I(B(graphics card)
* $B%M%C%H%o!<%/!&%$%s%?%U%'!<%9!&%+!<%I(B(network interface card)

### $B"!%O!<%I%&%'%"$N9=@.(B(hardware components)

$B%a%b%j!"#C#P#U!"%G%P%$%9$O!"%P%9(B(bus)($B%7%9%F%`!&%P%9(B(system bus))$B$rDL(B
$B$8$F@\B3$5$l$F$$$k!#(B
![$B?^#1!!%P%9$K$h$j@\B3$5$l$?#C#P#U!](./$BJB9T!&JBNs!&J,;6%W%m%0%i%_%s%0(B_concurrent,parallel,and distributed programming_files/hard-components.png)

**$B?^(B?$B!!%P%9$K$h$j@\B3$5$l$?#C#P#U!"%a%b%j!"%G%P%$%9(B(CPU, memory, and I/O devices connected with a bus)**

$B%P%9(B(bus)$B!'2?K\$+$NG[@~$NB+(B

$B%"%I%l%9%P%9(B (address bus)
:   $B%a%b%j$N%"%I%l%9$r<($9$?$a$N@~(B

$B%G!<%?%P%9(B (data bus)
:   $B%G!<%?$rAw$k$?$a$N@~(B

$B%3%s%H%m!<%k%P%9(B (control bus)
:   $B$=$NB>!"@)8fMQ$N@~(B

### $B"!%G%P%$%9!&%3%s%H%m!<%i(B(device controller)

$B3F%G%P%$%9$H(BCPU $B$G

$BNc!'%-!<%\!<%IMQ$N%3%s%H%m!<%i$NF/$-(B

$B%G!<%?$,!"EE5$?.9f$J$I$N7A$GAw$i$l$F$/$k!#%3%s%H%m!<%i$NCf$N%l%8%9%?(B(register)
$B!J>.MFNL$N%a%b%j!K$KJ]B8$5$l!#(B

### $B"!(BCPU$B$H%G%P%$%9$N4V$N%G!<%?$N

CPU $B$+$i8+$($k>l=j(B

1. $B%G%P%$%9!&%3%s%H%m!<%i$,(B I/O $B6u4V$K$"$j!"%]!<%HHV9f(B(port number)$B$H(B
   $B8F$P$l$kHVCO$,?6$i$l$F$$$k!#(BCPU $B$,!"%]!<%HHV9f$r;XDj$7$FF~=PNOL?Na(B(I/O
   instruction)$B$r- $B%G%P%$%9!&%3%s%H%m!<%i$,!"IaDL$N%a%b%j$HF1$86u4V$K$"$j!"%a%b%jHVCO(B
     (memory address)$B$,?6$i$l$F$$$k!#(BCPU $B$,!"$=$NHVCO$XIaDL$N%m!<%IL?Na(B
     (load instruction)$B$d%9%H%"L?Na(B(store instruction)$B$G%"%/%;%9$9$k$H!"%3%s(B
     $B%H%m!<%i$N%l%8%9%?$NFbMF$,FI$\_=q$-$G$-$k!#(BMMIO (Memory mapped I/O).

$BF~=PNO$N;~$K(B CPU $B$,F/$/$+$I$&$+(B

1. CPU $B$,F~=PNOL?Na(B(I/O instruction)$B!"$"$k$$$O!"%m!<%IL?Na(B(load
   instruction)$B$d!?%9%H%"L?Na(B(store instruction)$B$r- DMA (Direct Memory Access)$B$d%P%9%^%9%?$H8F$P$l$k5!4o$,$"$j!"$=$N(B
     $B5!4o$,(BCPU $B$,IaDL$KL?Na$rh$C

### $B"!%]!<%j%s%0$H3d$j9~$\_(B(polling and interrupt)

CPU $B$NB.EY$KHf$Y$F!"%G%P%$%9$NB.EY$OCY$$!#(B

* $BF~=PNO$N40N;$rBT$C$F$$$k$H(B CPU $B$NG=NO$,L5BL$K* $BJ#?t$NFHN)$7$?%G%P%$%9$O!"F1;~$KF0$+$7$?$$!#(B
  * $B$"$k%W%m%;%9$,%G%P%$%9$X$NF~=PNO$r9T$J$$$?$$;~!"(BCPU $B$,$=$N=hM}$K(B
    $B$D$-$C$-$j$K$J$C$F$7$^$&$H!"B>$N%W%m%;%9$^$G@h$K?J$a$J$/$J$k!#(B

$B2r7h:v(B

$B%]!<%j%s%0(B(polling)
:   $B<~4|E\*(B(periodic)$B$K%G%P%$%9!&%3%s%H%m!<%i$N>uBV$r%A%'%C%/$9$k!#(B

    * $B<~4|$,C;$$$H!"%A%'%C%/$N%X%C%I$,B?$/$J$k$,!"%G%P%$%9$H$N1~Ez$O$h(B
      $B$/$J$k!#(B
    * $B<~4|$,D9$$$H!"$=$N5U!#(B

$B3d$j9~$\_(B(interrupt)
:   $BF~=PNO$,2DG=$K$J$C$?!?(BDMA$BE>Aw$,40N;$7$?;~$K%G%P%$%9$,(BCPU$B$KCN$i$;$k!#(B

    * $BC10L$,9S$$;~$K$O!"%]!<%j%s%0$h$j$h$$!#(B
    * $B3d$j9~$\_$,:Y$+$9$.$k!JKhIC?t(B1000$B0J>e!K$H!"3d$j9~$\_=hM}$N(B
      $B%\*!<%P%X%C%I$,L5;k$G$-$J$/$J$k!#(B
    * $B%W%m%0%i%\_%s%0$,Fq$7$$!#(B

$B3d$j9~$\_$N%?%$%\_%s%0(B

$BF~NO%G%P%$%9(B(input device)
:   $B%3%s%H%m!<%i$O!"F~NO%G!<%?$,E~Ce$9$k$H!"@)8f%P%9$N3d$j9~$\_MW5a(B(IRQ,
    Interrupt Request)$B?.9f@~$r(B1$B$K$9$k!#(B
    DMA$B$r;H$C$F$$$k;~$K$O!"%a%b%j$X$N%3%T!<$,40N;$7$?;~$K(B
    $B?.9f@~$r(B1$B$K$9$k!#(B

$B=PNO%G%P%$%9(B(output device)
:   $B%3%s%H%m!<%i$O!"=PNOMQ%P%C%U%!(B(output buffer)$B$,6u(B(empty)$B$K$J$k$H!"(B
    $B3d$j9~$\_MW5a?.9f@~$r(B1$B$K$9$k!#(B

CPU $B$O!"3d$j9~$\_MW5a$r

### $B"!(BOS$B$N>eH>J,$H2J,(B(top half and bottom half)

![$B?^(B? $B%f!<%6!&%b!<%I$N%f!<%6!&%W%m%;%9!](./$BJB9T!&JBNs!&J,;6%W%m%0%i%_%s%0(B_concurrent,parallel,and distributed programming_files/os-top-half-bottom-half.png)

**$B?^(B?$B!!(BOS$B$N>eH>J,$H2J,(B**
$B%+!<%M%k!&%b!<%I$N%f!<%6!&%W%m%;%9$H3d$j9~$\_%O%s%I%i$,6&M-%G!<%?$r%"%/%;(B
$B%9$9$k!#(B

$BCm0U(B: Linux $B$G$O!"(Btop half $B$H(B bottom half $B$rJL$N0UL#$G;H$C$F$$$k!#(B
[$B>pJs2J3XN`!V%\*%Z%l!<%F%#%s%0%7%9%F%`(BII$B!W$N;qNA(B](https://www.coins.tsukuba.ac.jp/~yas/coins/os2-2022/2023-01-20/index.html#interrupt-top-bottom)
$B;2>H!#(B

### $B"!Aj8\_GS=|(B(mutual exclusion)

**$BAj8\_GS=|(B(mutual exclusion)**$B!'(B
$B$"$k;q8;$r%"%/%;%9$G$-$k

$B%W%m%0%i%`$N;zLL>e!"Aj8\_GS=|$,I,MW$JItJ,$r(B
**$B:]$I$$ItJ,(B(critical section)**
(
**$B%/%j%F%#%+%k%;%/%7%g%s(B**
)
$B$H$$$&!#(B

### $B"!3d$j9~$\_6X;\_(B(disabling interrupts)

CPU$B$K$O!"3d$j9~$\_$r6X;\_(B/$B5v2D$9$kL?Na$,$"$k!#(B

$BNc(B: x86

```
     di		# disable interrupts
     ....
     ei		# enable interrupts

```

$BC10l%W%m%;%C%5$G$O!"3d$j9~$\_6X;\_$r;H$C$FAj8\_GS=|$ruBV$G!"<+J,$,F0$$$F$$$l$P!"B>$N%b%8%e!<%k$,F0$/$3$H$O$"$jF@$J$$!#(B

$B3d$j9~$\_6X;\_$O!"7Z$$(B(lightweight)$B!#(BCPU$B$NL?Na$G(B1$BL?Na$+$i?tL?Na$G

$B%^%k%A%W%m%;%C%5$G$O!"3d$j9~$\_6X;\_$r;H$C$FAj8\_GS=|$r

### $B"!3d$j9~$\_%O%s%I%i(B($B3d$j9~$\_6X;\_$J$7(B==$B%P%0F~$j(B) (interrupt hander without disabling interrupts (with a bug))

```
int shared_resource ;

user_process()
{
    int x;
    x = shared_resource ;
    x = x + 1 ;
    shared_resource = x ;
}

interrupt_handler()
{
    int x;
    x = shared_resource ;
    x = x + 1 ;
    shared_resource = x ;
}

```

### $B"!3d$j9~$\_%l%Y%k(B(Interrupt level)

PDP-11 $B$K$O!"3d$j9~$\_6X;\_$N%l%Y%k$,(B 7 $BCJ3,(B(3$B%S%C%H(B)$B$"$C$?!#(B
SPL (Set Priority Level) $BL?Na!#(B

```
    splhigh(); /* $B3d$j9~$_6X;_(B disable interrupt */
    $B!c:]$I$$ItJ,!#(Bcritical section.$B!d(B
    spl0(); /* $B3d$j9~$_5v2D(B enable interrupt */

```

### $B"!3d$j9~$\_%O%s%I%i(B($B3d$j9~$\_6X;\_M-$j(B)(interrupt hander with disabling interrupts (bug fixed))

$B>e$N%W%m%0%i%`$r=q$-D>$9!#(B

```
int shared_resource ;

user_process()
{
    int x;
    splhigh();
    x = shared_resource ;
    x = x + 1 ;
    shared_resource = x ;
    spl0();
}

interrupt_handler()
{
    int x;
    splhigh();
    x = shared_resource ;
    x = x + 1 ;
    shared_resource = x ;
    spl0();
}

```

### $B"!B?=E3d$j9~$\_(B(multiple interrupt)

$BB?=E$N3d$j9~$\_$r5v$9!#(B

```
x = spltty(); /* $B3d$j9~$_%l%Y%k$r(B TTY $B%l%Y%k$K>e$2$k!#(B
                 Block interrupts from TTY devices (IPL_TTY). */

    $B!c$3$N4V$O!"(BIPL_TTY $B%l%Y%k0J2<$K$D$$$FAj8_GS=|$5$l$k!#(B
      Mutual exclusion for IPL_TTY and lower. $B!d(B

spl(x); /* $B3d$j9~$_%l%Y%k$r85$K$b$I$9!#(B
           Restore the system priority level to the previous one. */

```

NetBSD man page: spl(), spl0(), splbio(), splclock(), splhigh(),
splvm(), spllock(), spllowersoftclock(), splnet(), splsched(),
splserial(), splsoftclock(), splsoftnet(), splsoftserial(),
splstatclock(), spltty(), splvm(), splx()

$BC10l%W%m%;%C%5$G$O!"3d$j9~$\_%l%Y%k$rD4@0$7$?J}$,8zN($,$h$$$7!"(B
$BJBNs@-$b9b$/$J$k!#$7$+$7!"(BSMP $B$G$O!"$3$NJ}K!$O;H$($J$$!#(B

$B%8%c%$%"%s%H!&%m%C%/(B(giant lock)$B!#(Bsplhigh() $B$KMj$C$?%W%m%0%i%\_%s%0!#(B

### $B"!3d$j9~$\_$+$i%a%C%;!<%8$X$NJQ49(B(translating interrupts into messages)

$B%+!<%M%k$N3d$j9~$\_=hM}$N%W%m%0%i%`$OFq$7$$!#(B
$B3d$j9~$\_$r%W%m%;%94VDL?.$KJQ49$7$F%a%C%;!<%8!&%Q%C%7%s%0$N@$3&$G$b$N$r9M(B
$B$($?$$!#(B

$B3d$j9~$\_6X;\_$N;~4V$,C;$/$J$j!"1~Ez@-(B(responsiveness)$B$,>e$,$k!#(B

$BK\Ev$N3d$j9~$\_6X;\_$d!"3d$j9~$\_%l%Y%k$K$h$kM%@hEYIU$1(B(prioritize)$B$,$G$-$J$/$J$k!#(B

## $B"#N}=,LdBj(B(exercise)1 $BJB9T!&JBNs!&J,;6%W%m%0%i%\_%s%0(B/concurrent,parallel,and distributed programming

$B$B%l%]!<%HDs=P%Z!<%8(B
$B$+$iDs=P$7$J$5$$!#(B

$B2sEz$O!"$3$N%Z!<%8$K4^$^$l$F$$$k!#(B
Wikipedia, ChatGPT, $B$=$NB>$N?.Mj$G$-$J$$%=!<%9$+$iF@$?FbMF$r%3%T!<$7$F2sEz$7$J$$$3$H!#(B

Answers are included in this page.
You should not copy the contents from untested sources,
including Wikipedia and ChatGPT.

### $B!zLdBj(B(101) $BJB9T%W%m%0%i%`$NFCD'(B

$B- $B$"$k%3%s%T%e!<%?$G(B2$B$D$NFHN)$7$?C`- $B$"$k%3%s%T%e!<%?$G(B2$B$D$N%W%m%;%9$r4^$`(B1$B$D$NJB9T%W%m%0%i%`$,F0:n$7$F$$$k!#(B

  Compare the following two items and write an important common thing and an important diffidence between these two items.

  * Two independent sequential programs are running in a computer.
  * A concurrent program that includes two processes is runningin a computer.

  ### $B!zLdBj(B(102) $BJ,;6=hM}(B(A)$B$NMxE@(B

  $B:#F|$Nl9g!"C`

In this class, we classify distributed processing into Type (A) and Type (B).
We often use distributed processing of Type (A) that is slower than sequential processing.
In this case, answer an important advantage of using the distributed processing over using the sequential processing.

### $B!zLdBj(B(103) $B%H!<%i%9(B

[4 x 3 $B$N(B 2 $B$B$G!"(B
$B3F%N!<%I$KNY@\$7$F$$$k%N!<%I?t$O!"$$$/$D$+!#(B
$B:GBg%[%C%W?t$O$$$/$D$+!#(B

In [the 4 x 3 tours](https://www.cs.tsukuba.ac.jp/~yas/cs/csys-2023/2023-04-14/index.html#torus),
how many neighbor nodes does each node have?
What is the max hop count?

### $B!zLdBj(B(104) $B$-$o$I$$ItJ,(B

$B>e$N(B[$B!V3d$j9~$\_%O%s%I%i(B($B3d$j9~$\_6X;\_M-$j(B)$B!W(B](https://www.cs.tsukuba.ac.jp/~yas/cs/csys-2023/2023-04-14/index.html#isr-di)$B$N%W%m%0%i(B
$B%`$K$D$$$F!"$-$o$I$$ItJ,(B(critical section)$B$O$I$3$+!"0u$r$D$1$J$5$$!#(B

In [the interrupt hander with disabling interrupts](https://www.cs.tsukuba.ac.jp/~yas/cs/csys-2023/2023-04-14/index.html#isr-di),
mark the critical section of the program.

### $B!zLdBj(B(105) $B3d$j9~$\_6X;\_$N8B3&(B

$BAj8\_GS=|$N
Last updated: 2023/04/14 16:28:05

 [Yasushi Shinjo](http://www.cs.tsukuba.ac.jp/~yas/) / <yas@cs.tsukuba.ac.jp>

![](chrome-extension://dbjibobgilijgolhjdcbdebjhejelffo/assets/icon.png)](https://www.cs.tsukuba.ac.jp/~yas/cs/csys-2023/2023-04-14/index.html#torus)
