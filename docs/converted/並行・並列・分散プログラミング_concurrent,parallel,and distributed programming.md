# 並行・並列・分散プログラミング/concurrent,parallel,and distributed programming

```
並行システム

                               システム情報系/情報工学域,
			       システム情報工学研究群/情報理工学位プログラム
			       システム情報工学研究科/コンピュータサイエンス専攻
                               新城 靖
                               <yas@cs.tsukuba.ac.jp>
```

このページは、次の URL にあります。
 `<http://www.cs.tsukuba.ac.jp/~yas/cs/csys-2023/2023-04-14>`
あるいは、次のページから手繰っていくこともできます。
 `<http://www.cs.tsukuba.ac.jp/~yas/cs/>`
 `<http://www.cs.tsukuba.ac.jp/~yas/>`

## ■今日の重要な話

用語の意義

* 並行 concurrent
* 並列 parallel
* 分散 distributed

歴史 history

* ＯＳと単一プログラミング／マルチプログラミング OS and sequential programming/ multiprogramming
* 同期通信プリミティブ。ロック、セマフォ、モニタ、ランデブ。
  Synchronization primitives. locks, semaphores, monitors, rendezvous.
* プログラミング言語による支援。
  Programming language support.
* SMP とスレッド。
  SMP and threads.

ハードウェア

* UMA (Uniform Memory Access), SMP (Symmetric Multiprocessor)
* NUMA (Non-uniform Memory Access)
* NORMA (No-Remote Memory Access)

割り込みと並行プログラミング
Interrupts and concurrent programming

* 割り込み禁止による相互排除。
  mutual exclusion by disabusing interrupts

## ■並行・並列・分散プログラミング(concurrent, parallel, and distributed programming)

### ◆逐次プログラミングと並行プログラミング(sequential and concurrent programming)

逐次 sequential
:   １度に１つの手続きが実行される

並行 concurrent
:   １度に複数の手続きが実行される

```
main()
{
	printf("hello, world!\n");
}
```

逐次プログラムでは、1度に1つの手続き(関数)(procedure(function))しか実行
されない。printf() が動くと main() は止まる。

複数の手続きを実行する主体は、「プロセス(process)」や「スレッド
(thread)」。

![縦軸時間、横軸空間、スレッドが協調している](./並行・並列・分散プログラミング_concurrent,parallel,and distributed programming_files/seq-con-threads-coordinate.png)

**図? 逐次プログラムと並行プログラムの動作(時間と空間の観点から)**

### ◆並列処理と分散処理の目的 (Objectives of parallel processing and distributed processing)

並列 parallel
:   １つの問題を（逐次処理より）速く(faster)解きたい

分散 distributed (A)
:   **離れていても心は１つ** sharing one heart between two separate lovers

分散 distributed (B)
:   1台のコンピュータのメモリに乗らないデータを扱いたい。
    (2次記憶と置換ながらなら動く。)

この授業では「分散 distributed (B)」は、並列の一種として扱う。
分散処理の目的として「分散 distributed (A)」を扱う。

「分散 distributed (A)」は、逐次処理より遅くなっても良い。
次のようなことを実現したい。

* フォールトトレランス fault torrance。
  要素の一部が故障していても(partial failure)でも動き続ける。
* 構成要素の漸進的な置換 incremental replacement of components。
  壊れた部品を取り換える。
  性能が足りなくなったら追加する。
* 人手のかかる処理を分担。
  例: DNS (Domain Name System)。

### ◆並行プログラミング（並列、分散、その他）の共通の話

* (プロセッサが複数) (multiple processors)
* プロセスが複数 multiple processes
* プロセス間の協調(coordination)が必要。同期(synchronization)、通信(communication)。
* 資源割り当て(resource allocation)、スケジューリング(scheduling )が重要。

単一プロセッサでの並行プログラミングもある。後述。
concurrent programming in a single processor.

### ◆並行プログラミングで必要な言語

２つの言語が必要

計算言語 computational languages
:   個々の活動を記述

    * C
    * Fortran

協調言語 coordination languages
:   統一されたプログラムに組み立てるための「糊(glue)」

    * Linda
    * (同期・通信ライブラリ)

Java など、１つの言語で計算と協調が書けるものもある。

## ■歴史 history

歴史的に重要な出来事と並行プログラミングを学ぶ意義。

講義の最後には、ここで現れるキーワードを理解できることを目標にする（今
日の段階では理解できないものがあってもよい）。

### ◆逐次プログラミングの発明 invention of sequential programming

ハードウェアは、本質的には並列。全部の素子が同時に動く。

プログラムカウンタの発明。プログラム内蔵方式。
ノイマン型コンピュータ。

逐次処理は非常に特殊

* 歴史的な都合。ハードウェアが高価だった。
  複数コンピュータを使うのは贅沢すぎる。
* **逐次プログラムの書きやすさ**。制限をつけた方がわかりやすい。
  学部1年生でもプログラムがかける。

当初のコンピュータに、ＯＳはない。

### ◆マルチプログラミング multiprogramming

１台のコンピュータのメモリに、同時に複数のプログラムをロードして切り替
えながら動作させる。

ハードウェアは、高い。

高いＣＰＵを有効に活用したい。

バッチ処理の誕生。入出力とＣＰＵ処理を「並列」動作させる。

![３つのジョブの逐次処理。各ジョブは、入力、処理、出力。](./並行・並列・分散プログラミング_concurrent,parallel,and distributed programming_files/batch-input-proc-output-seq.svg)

**図? 3つのジョブの逐次処理 (Executing three jobs sequentially)**
![ジョブが３つ、入力、処理、出力、異なるものは重なってもよい。](./並行・並列・分散プログラミング_concurrent,parallel,and distributed programming_files/batch-input-proc-output.svg)

**図? バッチ処理における CPU と入出力装置の並列動作 (parallel processing of CPU and I/O in batch processeing)**

プロセスの概念の確立。プロセスとプログラムの分離。
一般のプログラミングは、逐次のまま。

ＯＳだけ並行プログラミング

* 難しい並行プログラミングをＯＳに閉じ込めて、残りは楽をする。
* ＯＳはがんばって作る

今でもＯＳの教科書には、セマフォやデッドロックの話が出ている。

Concurrent Pascal, Solo。

ＯＳの実装では、実際には、「割り込み禁止」という軽量の相互排除命令が多
用された。

### ◆単一プロセッサ(a single processor)

単一プロセッサ。
技術的に確立している。
![CPU、メモリ、I/O、OS、アプリケーション](./並行・並列・分散プログラミング_concurrent,parallel,and distributed programming_files/single-processor.svg)

**図? 単一プロセッサ (a single processor system)**

### ◆Unix fork-exit-wait

ユーザレベルの命令の例

* fork()
* exit()
* wait()

fork join model

### ◆TSS (Time sharing system)

Time sharing system。

１台の中央の大型コンピュータ(mainframe)に、複数の「（文字）端末
(terminal)」を接続。

端末を使っている人からすると専有しているように見える。

TSS で複数のアプリケーションを同時に走らせる。
CPU が貴重な時代。CPU を遊ばせない。

![メインフレーム１台、端末ｎ台](./並行・並列・分散プログラミング_concurrent,parallel,and distributed programming_files/mainframe-terminals.png)

**図? メインフレームと端末(a mainframe and terminals)**

### ◆Virtual Machine

１台のメインフレームに、同時に複数のＯＳを走らせるのが始り。
TSS の実装方法の１つでもあった。

最近は、
コンピュータの高速化で、性能が余ってきた。もともとハードウェアｎ台でやっ
ていた仕事を、ハードウェアとしては１台に集約する。並列処理の逆。

![図? サーバ３台、ＯＳ３種類、アプリケーションそれぞれ２つ](./並行・並列・分散プログラミング_concurrent,parallel,and distributed programming_files/virtual-machine-server-consolidation-before.png)

**図? 仮想計算機によるサーバの集約(集約前) (before server consolidation by virtual machines)**
![図? ハードウェア1台、ＯＳ３種類、アプリケーションそれぞれ２つ](./並行・並列・分散プログラミング_concurrent,parallel,and distributed programming_files/virtual-machine-server-consolidation-after.png)

**図? 仮想計算機によるサーバの集約(集約後) (after server consolidation by virtual machines)**

1999年VMware Workstation 以降、パソコン用の VM も広く使われる。

### ◆データベース(database)

プログラムとデータを分離。データを複数のプログラムで共有(share)。
データを中心に考える。
データに integrity を持たせる。
integrity を満たしたデータだけを、きちんと
永続的(persistent)に保存する。

### ◆トランザクション(transaction)

複数のデータベースへの問い合わせ（検索、更新）を、できるだけ「並行
(concurrent)」に実行する。
効率のため。

最終結果は、１つひとつ逐次的(sequential)にやったものと同じ。
serializability。
integrity を満たす。

### ◆Local Area Networkとworkstation

Sun Workstation。

資源を共有したい。プリンタ。ディスク。

ディスクレス・ワークステーション。

Socket API、X Window、
NFS, NIS, RPC 出現。

### ◆Socket API

もともと Unix 4.2 BSD 用。
socket(), listen(), accept(), connect(), send(), recv(), select()。

複数の通信プロトコル(TCP/IP以外も)を扱える。

### ◆X Window

X Window。ウインドウのプログラミングは、本質的に並行(inherently concurrent)。
X Windowの実装は、クライアント・サーバ・モデル(client server model)に基づく。
ただし、後に、モデルを変更した。
サーバからクライアントへのイベント(events)の送信を付けた。
リスナ・パタン(listener pattern)へと発展。

### ◆Remote Procedure Call(RPC)

遠隔手続呼出し。プロセス間通信(interprocess communication)だが、一見、
手続き呼び出し(procedure calls)に見える。

RPC は、NFS (Network File System) の実装で使われている。
coins Linux azalea PC や violet サーバ、
全学計算機 icho01, icho02, kiri で、
どのコンピュータを使っても、自分のホームディレクトが見えるのは、NFS を
使っている。

NFS のために UID (user id) とパスワードを共有するために使われたのが
NIS (Network Information System)。

### ◆並行プログラミング言語

* ペトリネット Petri Net
* CSP (Communicating Sequential Processes)
* Actors
* Concurrent Pascal, Distributed Processes(言語の名前)
* Ada
* PLITS, Synchronizing Resources, Cell
* Argus

### ◆Ada

Ada。アメリカ国防省(US DoD, Department of Defence)
で仕様を決めた組み込みシステム(embedded systems)用の
プログラミング言語。

* 仕様(specification)（インタフェース(interface)）と実現(implementation)の分離
* プロセス生成
* ランデブ(rendezvous)によるプロセス間通信

### ◆プログラミング言語が提供する概念

並行実行(concurrent execution)。同期(synchronization)。非決定性
(non-determinism)。ガード付きコマンド(guarded commands)。

哲学者の食事問題(dining philosophers problem)。生産者消費者問題
(producer-consumer problem)／有限バッファ問題(bounded buffers)。デッド
ロック(deadlock)。

初期の実装は、全部コルーチン(coroutine)。

### ◆オブジェクト指向プログラミング(object oriented programming)

プログラムをオブジェクト(objects)の集合で書く。
オブジェクトは、人間のように、自律(autonomous, autonomic)している。
オブジェクトの内部のデータは外から触れない。データベースの逆。
オブジェクトの内部をアクセスするには、メッセージ(message)を送るしかない。

オブジェクト指向プログラミングは、本質的には並行プログラミング。
実際問題は単に手続き呼出しの実装が多い。

obj1.method1();

Smalltalk 80

オブジェクト指向データベース(object-oriented databases)の矛盾。

### ◆ORB

Object Request Broker。複数の言語を繋ぎたい。
オブジェクト指向が入った RPC 。

### ◆通信ライブラリ(Communication Library)

* PVM, Parallel Virtual Machine
* MPI, Message Passing Interface

### ◆パソコン(Personal Computers)

比較的新しい。

### ◆CP/M (Control Program for Microcomputers)

パソコン用の（フロッピ・）ディスクＯＳ（(floppy)Disk Operating System）。
一度に１つだけプログラムが動く。
キーボード入出力、フロッピ・ディスクのＤＭＡ転送完了には割り込みを使う。

### ◆Macintosh Multi-finder

「パソコンで」、一度に複数のプログラムを切り替えながら使える。

### ◆MS-DOS

CP/M に、Unix 的な機能を入れた。

1. 階層化ディレクトリ(hierarchical directories)。mkdir, chdir
2. 子プロセスは作れる(child processes)。（自分は止まる。）

### ◆MS Windows

「パソコンで」、複数のプログラムを同時に動かしても、うまく動くようになっ
た。

MS Windows 95 は、内部的には、COM/OLE と呼ばれる ORB の固まりで作られ
ている。

パソコンでは、保護の概念が希薄。

### ◆マルチプロセッサ(a multi processor)

[単一プロセッサで](https://www.cs.tsukuba.ac.jp/~yas/cs/csys-2023/2023-04-14/index.html#single-processor-computer) CPU を増やす。
![CPUx3個、メモリ、I/O、OS、アプリケーション](./並行・並列・分散プログラミング_concurrent,parallel,and distributed programming_files/multi-processor.svg)

**図? マルチプロセッサ (a mult-processor)**

### ◆Intel Hyperthreading

CPUのプログラム・カウンタ回りだけ増やしたもの。

### ◆Multi-core

１つのチップに、複数の CPU を載せる。

今の段階では、単に、CPU 2 個あるものを 1 個にまとめたようなもの。
昔の SMP −＞ UMA の再現。コア数、チップ数が増えるに従い、
不均質になる。

### ◆Internet

TCP/IPの４層モデル。
OSI の７層モデル(seven layer model)より古い。

クライアント・サーバ・モデル(client server model)。

inetd (Internet daemon)。

### ◆UUCP (Unix-to-Unix Copy)

貧乏人の Internet。poor man's Internet

今の用語だとモデム(modem)によるダイヤルアップ(dial up)接続を用いた
peer-to-peer (P2P) 型のファイル転送(file transfer)。
電子メール(email)とネットニュース(netnews, Usenet)の記事を運ぶ。

ニュースシステム(news system)の仕組みは、分散システムの優れた例になっている。

### ◆ftp

ソフトの配布と論文投稿。
anonymous ftp。archie.
夜中に走らせるのが礼儀。

### ◆World Wide Web

文字たけでなく、絵が出る。ヘルパーで音も出る。

クライアント・サーバ・モデル(client server model)。
バッチ処理風(batch processing like)。

### ◆CGI

Common Gateway Interface。

最近では、多くの人が、CGI ではじめて並行プログラミングに出会う。

ロックしないとダメ。デッドロックが起り得る。

### ◆Java Applet

Webブラウザで、アニメーションを行うために登場。

### ◆Java Servlet

重たい fork() を避ける。

### ◆XML Web Service

ORB の次の世代の RPC。

HTML。XML。HTTP。SOAP。

### ◆Representational state transfer (REST)

XML Web Service の次の世代の RPC。

### ◆P2P

Peer-to-peer 。

クライアント・サーバの意義が大事。
クライアント・サーバが現れる前の状況に戻ってはいけない。

Single Point of Failure を避けるという考え方はよい。

### ◆クラウド・コンピューティング(cloud computing)

* データセンター(data centers)に資源を集中させる
* 複数企業で資源を共有する。

[メインフレームによるTSS](https://www.cs.tsukuba.ac.jp/~yas/cs/csys-2023/2023-04-14/index.html#tss)の再来とも言える。

## ■ハードウェア / hardware

### ◆シングルプロセッサと集中型システム / single processors and centralized systems

シングルプロセッサは、１台のコンピュータにプロセッサが CPU が 1 つ、メ
モリも 1つ。

ネットワークで接続された複数のコンピュータ(multiple computers that are
connected with a network)から構成される分散システム(distributed
systems)と対比する時には、集中型システム(centralized systems))と呼ばれ
る。

技術的に確立している。

![CPU、メモリ、I/O、OS、アプリケーション](./並行・並列・分散プログラミング_concurrent,parallel,and distributed programming_files/single-processor.svg)

**図? 単一プロセッサ (a single processor system)**

### ◆並列コンピュータ(parallel computers)

Flynn の分類 (Flynn's taxonomy)

* SISD, Single Instruction, Single Data
* SIMD, Single Instruction, Multiple Data
* MISD, Multiple Instruction, Single Data
* MIMD, Multiple Instruction, Multiple Data

MIMD の分類

* 共有メモリがある(with shared memory)
* 共有メモリがない(without shared memory)

Machシステムでの分類 ( Mach operating system kernel, Mach microkernel )

* 共有メモリがある(with shared memory)
  + アクセスが均質: UMA (Uniform Memory Access), SMP (Symmetric Multiprocessor)
  + アクセスが不均質(100倍くらい): NUMA (Non-uniform Memory Access)
* 共有メモリがない: NORMA (No-Remote Memory Access)。

### ◆共有メモリ型マルチプロセッサ、SMP (Shared memory multiprocessor)

![(CPU+Cache)*n+メ モリ](./並行・並列・分散プログラミング_concurrent,parallel,and distributed programming_files/shared-memory-multiprocesor.png)

**図? 共有メモリ型マルチプロセッサ(バス共有) (Shared memory multiprocessor (with a shared bus))**

* Symmetric multiprocessor (SMP)とも言う。メモリへのアクセス時間がどの場所も対称的で均質(symmetric)。
* 分散システムには分類しないのが普通。
  集中システムのプログラムがそのまま動作するので。
* キャッシュの親和性(cache affinity)まで考えると分散的な技術がいる。
  メモリの整合性(memory consistency)まで考えると、本当はかなり難しい。
* マルチコアCPU (multi-core CPU)は、単体でSMP分類される。歴史的には古い。

### ◆クロスバースイッチ(crossbar switch)

![n*CPU-n*Memory](./並行・並列・分散プログラミング_concurrent,parallel,and distributed programming_files/crossbar-switch-multiprocesor.png)

**図? 共有メモリ型マルチプロセッサ(クロスバースイッチ) (shared memory multiprocessor with a crossbar switch)**
複数のCPUが別のメモリに同時にアクセスできる。
同じメモリならバスと同様に衝突する。

### ◆非均質共有メモリ型マルチプロセッサ(shared memory multiprocessor with non-uniform memory access)

![CPU、メモリ、相互結合ネットワーク](./並行・並列・分散プログラミング_concurrent,parallel,and distributed programming_files/non-uniform-memory-access.png)

**図? 非均質共有メモリ型マルチプロセッサ (shared memory multiprocessor with non-uniform memory access)**
相互結合ネットワークで、遠隔のメモリを CPU から直接アドレスでアクセス
できる。ただし、速度は 100 倍くらい遅い。

### ◆LANに接続されたコンピュータ群(multiple computers connected to a LAN)

![PC*3--hub](./並行・並列・分散プログラミング_concurrent,parallel,and distributed programming_files/pc-swiching-hub.png)

**図? LANに接続されたPC**
[NORMA](https://www.cs.tsukuba.ac.jp/~yas/cs/csys-2023/2023-04-14/index.html#norma)の一種。
機種が違う(heterogeneous)こともある。

### ◆トーラス Torus

![3x4 2d torus](./並行・並列・分散プログラミング_concurrent,parallel,and distributed programming_files/torus-2d.png)

**図? 2次元トーラス**
格子状だが、端が反対側とつながっている。
世の中、3次元なので、2次元トーラスの配線は簡単。

3次元以上のトーラスも可能だが、配線が大変になる。

### ◆ハイパーキューブ Hypercube

![ハイパーキューブ(1次元-4次元)](./並行・並列・分散プログラミング_concurrent,parallel,and distributed programming_files/hypercube.svg)

**図? ハイパーキューブ(1次元-4次元)**
2次元トーラスよりも、ノード間のホップ数が少ない。

配線が大変になる。

## ■割り込み(interrupt)

マルチプロセッサではない、単一CPUのシステムで、効率的に並行プログラム
を記述するための仕組み。
CPU と周辺装置の並列処理に使う。
ハードウェアの直接的なサポートがある。

割り込みのプログラミングは、非常に難しい。デバッガが使えない。
printf() もつかえない。

ただし、並行性の記述については、スレッドのデッドロックよりは、場合によっ
ては簡単かもしれない。

もともとスレッドのプログラムを割り込みのプログラムに書き換えるのは
難しい。

### ◆周辺装置(peripheral devices)

入出力装置(デバイス)、デバイス(device)
とは、コンピュータの箱の中に内蔵されているハードウェアの部品やケーブル
で外で接続する部品。
普通は、CPU とメモリ以外のことを指す。
周辺装置(peripheral device)、
入出力装置(IO device)とも呼ばれる。

* ハードディスク(hard disks)
* キーボード(keyboard)
* マウス(mouse)
* グラフィクス・カード(graphics card)
* ネットワーク・インタフェース・カード(network interface card)

### ◆ハードウェアの構成(hardware components)

メモリ、ＣＰＵ、デバイスは、バス(bus)(システム・バス(system bus))を通
じて接続されている。
![図１　バスにより接続されたＣＰＵ、メモリ、デバイス](./並行・並列・分散プログラミング_concurrent,parallel,and distributed programming_files/hard-components.png)

**図?　バスにより接続されたＣＰＵ、メモリ、デバイス(CPU, memory, and I/O devices connected with a bus)**

バス(bus)：何本かの配線の束

アドレスバス (address bus)
:   メモリのアドレスを示すための線

データバス (data bus)
:   データを送るための線

コントロールバス (control bus)
:   その他、制御用の線

### ◆デバイス・コントローラ(device controller)

各デバイスとCPU で実行されるプログラムとデバイスとり橋渡しをする機器。

例：キーボード用のコントローラの働き

データが、電気信号などの形で送られてくる。コントローラの中のレジスタ(register)
（小容量のメモリ）に保存され。

### ◆CPUとデバイスの間のデータの受け渡しの方法

CPU から見える場所

1. デバイス・コントローラが I/O 空間にあり、ポート番号(port number)と
   呼ばれる番地が振られている。CPU が、ポート番号を指定して入出力命令(I/O
   instruction)を実行すると、I/O 空間にあるレジスタの内容が読み書きできる
   (I/O 空間を示す信号線が1になる)。
2. デバイス・コントローラが、普通のメモリと同じ空間にあり、メモリ番地
   (memory address)が振られている。CPU が、その番地へ普通のロード命令
   (load instruction)やストア命令(store instruction)でアクセスすると、コン
   トローラのレジスタの内容が読み書きできる。MMIO (Memory mapped I/O).

入出力の時に CPU が働くかどうか

1. CPU が入出力命令(I/O instruction)、あるいは、ロード命令(load
   instruction)や／ストア命令(store instruction)を実行する。
2. DMA (Direct Memory Access)やバスマスタと呼ばれる機器があり、その
   機器がCPU が普通に命令を実行している合間をぬって一時的にバスを乗っ取り、
   データをメモリにコピーする。

### ◆ポーリングと割り込み(polling and interrupt)

CPU の速度に比べて、デバイスの速度は遅い。

* 入出力の完了を待っていると CPU の能力が無駄に捨てられる。
* 複数の独立したデバイスは、同時に動かしたい。
* あるプロセスがデバイスへの入出力を行ないたい時、CPU がその処理に
  つきっきりになってしまうと、他のプロセスまで先に進めなくなる。

解決策

ポーリング(polling)
:   周期的(periodic)にデバイス・コントローラの状態をチェックする。

    * 周期が短いと、チェックのヘッドが多くなるが、デバイスとの応答はよ
      くなる。
    * 周期が長いと、その逆。

割り込み(interrupt)
:   入出力が可能になった／DMA転送が完了した時にデバイスがCPUに知らせる。

    * 単位が荒い時には、ポーリングよりよい。
    * 割り込みが細かすぎる（毎秒数1000以上）と、割り込み処理の
      オーバヘッドが無視できなくなる。
    * プログラミングが難しい。

割り込みのタイミング

入力デバイス(input device)
:   コントローラは、入力データが到着すると、制御バスの割り込み要求(IRQ,
    Interrupt Request)信号線を1にする。
    DMAを使っている時には、メモリへのコピーが完了した時に
    信号線を1にする。

出力デバイス(output device)
:   コントローラは、出力用バッファ(output buffer)が空(empty)になると、
    割り込み要求信号線を1にする。

CPU は、割り込み要求を受け付けると、現在実行中の処理を中断して、
割り込みサービスルーチン(Interrupt Service Routine)
あるいは
割り込みハンドラ(interrupt handler)
と呼ばれるプログラムを実行する。
割り込み処理ルーチンでは、実際に入力命令を実行したり、
次のデータを出力を開始する。
最後に、割り込み処理から復帰する命令を実行する。すると、先ほど中断してい
た処理が再開される。

### ◆OSの上半分と下半分(top half and bottom half)

![図? ユーザ・モードのユーザ・プロセス、カーネル・モードのユーザ・プロセス、割り込みハンドラ、デバイス、共有データ](./並行・並列・分散プログラミング_concurrent,parallel,and distributed programming_files/os-top-half-bottom-half.png)

**図?　OSの上半分と下半分**
カーネル・モードのユーザ・プロセスと割り込みハンドラが共有データをアクセ
スする。

注意: Linux では、top half と bottom half を別の意味で使っている。
[情報科学類「オペレーティングシステムII」の資料](https://www.coins.tsukuba.ac.jp/~yas/coins/os2-2022/2023-01-20/index.html#interrupt-top-bottom)
参照。

### ◆相互排除(mutual exclusion)

**相互排除(mutual exclusion)**：
ある資源をアクセスできる主体(スレッド)の数を多くても１つにする。

プログラムの字面上、相互排除が必要な部分を
**際どい部分(critical section)**
(
**クリティカルセクション**
)
という。

### ◆割り込み禁止(disabling interrupts)

CPUには、割り込みを禁止/許可する命令がある。

例: x86

```
     di		# disable interrupts
     ....
     ei		# enable interrupts
```

単一プロセッサでは、割り込み禁止を使って相互排除を実現できる。
割り込み禁止の状態で、自分が動いていれば、他のモジュールが動くことはあり得ない。

割り込み禁止は、軽い(lightweight)。CPUの命令で1命令から数命令で実装可能である。

マルチプロセッサでは、割り込み禁止を使って相互排除を実現できない。
In a multiprocessor system, it is impossible to realize mutual exclusion by disabling interrupts.

### ◆割り込みハンドラ(割り込み禁止なし==バグ入り) (interrupt hander without disabling interrupts (with a bug))

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

### ◆割り込みレベル(Interrupt level)

PDP-11 には、割り込み禁止のレベルが 7 段階(3ビット)あった。
SPL (Set Priority Level) 命令。

```
    splhigh(); /* 割り込み禁止 disable interrupt */
    ＜際どい部分。critical section.＞
    spl0(); /* 割り込み許可 enable interrupt */
```

### ◆割り込みハンドラ(割り込み禁止有り)(interrupt hander with disabling interrupts (bug fixed))

上のプログラムを書き直す。

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

### ◆多重割り込み(multiple interrupt)

多重の割り込みを許す。

```
x = spltty(); /* 割り込みレベルを TTY レベルに上げる。
                 Block interrupts from TTY devices (IPL_TTY). */

    ＜この間は、IPL_TTY レベル以下について相互排除される。
      Mutual exclusion for IPL_TTY and lower. ＞

spl(x); /* 割り込みレベルを元にもどす。
           Restore the system priority level to the previous one. */
```

NetBSD man page: spl(), spl0(), splbio(), splclock(), splhigh(),
splvm(), spllock(), spllowersoftclock(), splnet(), splsched(),
splserial(), splsoftclock(), splsoftnet(), splsoftserial(),
splstatclock(), spltty(), splvm(), splx()

単一プロセッサでは、割り込みレベルを調整した方が効率がよいし、
並列性も高くなる。しかし、SMP では、この方法は使えない。

ジャイアント・ロック(giant lock)。splhigh() に頼ったプログラミング。

### ◆割り込みからメッセージへの変換(translating interrupts into messages)

カーネルの割り込み処理のプログラムは難しい。
割り込みをプロセス間通信に変換してメッセージ・パッシングの世界でものを考
えたい。

割り込み禁止の時間が短くなり、応答性(responsiveness)が上がる。

本当の割り込み禁止や、割り込みレベルによる優先度付け(prioritize)ができなくなる。

## ■練習問題(exercise)1 並行・並列・分散プログラミング/concurrent,parallel,and distributed programming

次の内容を含む「テキスト」ファイルを作成し、
[レポート提出ページ](https://www.cs.tsukuba.ac.jp/~yas/cs/csys-2023/reports.html)
から提出しなさい。

回答は、このページに含まれている。
Wikipedia, ChatGPT, その他の信頼できないソースから得た内容をコピーして回答しないこと。

Answers are included in this page.
You should not copy the contents from untested sources,
including Wikipedia and ChatGPT.

### ★問題(101) 並行プログラムの特徴

次の2つを比較し、重要な共通点を１つと重要な相違点を１つ述べなさい。

* あるコンピュータで2つの独立した逐次プログラムが動作している。
* あるコンピュータで2つのプロセスを含む1つの並行プログラムが動作している。

Compare the following two items and write an important common thing and an important diffidence between these two items.

* Two independent sequential programs are running in a computer.
* A concurrent program that includes two processes is runningin a computer.

### ★問題(102) 分散処理(A)の利点

今日の授業では、分散処理を (A) と (B) の 2種類に分けた。
このうち、(A) は、逐次処理より遅いことがある。
この場合、逐次処理と比較して分散処理を利用する重要な利点を１つ答えなさい。

In this class, we classify distributed processing into Type (A) and Type (B).
We often use distributed processing of Type (A) that is slower than sequential processing.
In this case, answer an important advantage of using the distributed processing over using the sequential processing.

### ★問題(103) トーラス

[4 x 3 の 2 次元のトーラス](https://www.cs.tsukuba.ac.jp/~yas/cs/csys-2023/2023-04-14/index.html#torus)で、
各ノードに隣接しているノード数は、いくつか。
最大ホップ数はいくつか。

In [the 4 x 3 tours](https://www.cs.tsukuba.ac.jp/~yas/cs/csys-2023/2023-04-14/index.html#torus),
how many neighbor nodes does each node have?
What is the max hop count?

### ★問題(104) きわどい部分

上の[「割り込みハンドラ(割り込み禁止有り)」](https://www.cs.tsukuba.ac.jp/~yas/cs/csys-2023/2023-04-14/index.html#isr-di)のプログラ
ムについて、きわどい部分(critical section)はどこか、印をつけなさい。

In [the interrupt hander with disabling interrupts](https://www.cs.tsukuba.ac.jp/~yas/cs/csys-2023/2023-04-14/index.html#isr-di),
mark the critical section of the program.

### ★問題(105) 割り込み禁止の限界

相互排除の実現に割り込み禁止を使うことの重要な限界を1つ述べなさい。
Write an important limitation of using disabling interrupts for
implementing mutual exclusion.

---

Last updated: 2023/04/14 16:28:05

 [Yasushi Shinjo](http://www.cs.tsukuba.ac.jp/~yas/) / <yas@cs.tsukuba.ac.jp>

![](chrome-extension://dbjibobgilijgolhjdcbdebjhejelffo/assets/icon.png)
