#* 実装型
◯int
◯ouble

◯vec2(x,y) 2次元ベクトル

◯vec4(x,y,z,w)
○hsva(h,s,v,a)
○rgba(r,g,b,a) 色

◯Sprite　スプライト定義

◯Player 自機

◯PB 自機の弾

◯PL 自機のレーザー

◯Effect エフェクト

◯Bullet 弾 vec2 r,vec2 v,vec2 a,double omega,vec4 color,int graphic,double size

◯LaserA レーザーA（まっすぐ） vec2 r,vec2 v,vec2 a,double omega,double fulcrum,double[] length,vec4[] color,int graphic,vec2 size

○　　　　　　　　　　　　　　　fulcrumは支点（デフォsize.yの半分）、length[i]の箇所の色をcolor[i]に設定する

◯LaserB レーザーB（直線）vec2 r,vec2 v,vec2 a,double omega,double fulcrum,double[] length,vec4[] color,int graphic,vec2 size 

○　　　　　　　　　　　　　　　fulcrumは支点（デフォ０）、rの実際の位置を表します

◯LaserC レーザーC（へにょり）vec2 r,vec2 v,vec2 a,double omega,double[] frame,vec4[] color,int graphic,vec2 size
                          
○                          r[\frame]でfフレーム経った跡の座標
                          
◯Enemy 敵 vec2 r,vec2 v,vec2 a,double omega,int graphic,double hp

◯BulletManager(Bullet|LaserA|LaserB|LaserC|Enemy 及び派生) 敵・弾の一括処理用 (内部:int[] 配列の縦横的な長さ) vec2[] rなど

◯Boss ボス

◯配列 例：\[2,3,4\]


*#
#* 定数、関数のメモ

◯弾(BulletManager)

例：BM\*5 そのまま複製

BM.v = 0.5 BMに格納されてる弾のv情報だけすべて0.5にする

BM.a.x\[0] += 0.01 BMに格納されている弾のうち\[0]領域のa.x情報に0.01足す
BM.r @= \[0:5:1]\*60 :BMのうち、\[i]領域のr情報を60\*i degだけ回す

BM.fire　：一斉に発射

弾パターンの関数（(面倒×使用頻度)の値が馬鹿高い弾幕パターンを事前に定義する）

絶対に使わない組み合わせのトークン共で専用演算子作るのも考える

○vertical　1なら斜め45度を追加

○way　　　　角度と個数

○radial　　円

○line　　　速度だけバラバラ

○winder　　時間をずらす


移動用

この手のは"そういうスレッド"を作らせてやらせる。面倒なので

○moveabs(r,v0,v1,f) ：絶対座標。速さv0から、fフレームかけて速さv1で到着する。
　　　　　　　　　　　　　　　　
                　　　　　　　　なんかの値が欠けてたらそこは補完する
                        
○moverel(r,v0,v1,f) ：相対座標（移動物から見た距離）


○move2abs(r,r1,r2,f) :エルミート曲線

○move2rel(r,r1,r2,f)


ランダム系関数

○irand(i,j)

○drand(x,y)

○srand() : -1か1

数学関数
○max(...),min(...),clamp(...)

○ceil(x),floor(x)

○sgn(x),abs(x) :sgnはvec2の偏角、absはvec2の長さとしても使える

○sin(x),cos(x),tan(x)

○sinh(x),cosh(x),tanh(x)

○asin(x),acos(x),atan(x)

○asinh(x),acosh(x),atanh(x)

○exp(x),ln(x),lb(x),lg(x),log(x,a)

*#
#* stat 文のメモ

◯文;文

◯文（改行）文

◯宣言 例：int x = 0

◯式　　例：x = 1+2 sin(4)

◯if文
○　　　if 式{}

○     elif 式{}
     
○     else{}
     
     
◯switch文

○　　 switch 式{
     
○     case 値:
     
○     ....
     
○     case 値:
     
○     case 値:
     
○     ....
     
○     default:
     
○     ....
     
○     }

◯while文 while 式{}

◯for文   for 変数 : 式 : 式 {}

◯foreach文　 foreach i in index{}

◯break文、continue文、pass文

◯return文、yield文

◯wait文　wait(n) = yieldをn回

◯when文 when 式{

○       start:
       
○       　　文章
       
○      while:
       
○      　　文章
       
○      end:
       
○      　　文章
         
○　　　}　

○　　　トリガー用。trueになったらstart、trueの間は1番目、falseになったらfinishの処理をする。
    
○  　　passすら書いてない場合は次のブロックの処理になる。


◯def文: def(){} 関数定義

◯class文 class(コンストラクタ用変数){} :上位クラス

*#

#*
exp：演算子のメモ

(ちょっと怪しい){
○m<t> : tフレーム後の値

使うたびにデータ更新（v.x<3> *= 15 →wait(15) v.x *= 15という中身のスレッドを立てる ）
  
値として使う場合

omega<t> : 最も近い過去のomegaのまんま
     
a<t> : 最も近い過去のaを基準に、v,a,omegaから計算 a<T+1> = a<T>@omega<T>
     
v<t> : 最も近い過去のvを基準に、v,a,omegaから計算 v<T+1> =(v<T>+a<T>)@omega<T> から計算
     
r<t> : 最も近い過去のrを基準に、r,v,a,omegaから計算 r<T+1> = r<T> + v<T>
}
  
○<e:n:h:l> :難易度別の数値用
     
○<eex:ex:abex> :同様

     
○x.m
○f()
     
○index[i]

○x++
     
○x--

○-x

○!x (not)
     
○~x

○++x
     
○--x

○type(x)　（キャスト）

○vec2@r (回転操作)
     
○x**y

○x*y

○x/y
     
○x//y
     
○x%y

○x+y
     
○x-y

○(x<<y)
     
○(x>>y)

○x<y
     
○x>y

○x<=y
     
○x>=y

○x == y
     
○x != y

○x & y x ^ y x | y
     
○x && y x ^^ y x || y

○x ? y : z

○i ~ j : k 　iとjをkで内分した値(配列可)

○\[i:j::k] （内包表記）iからjまでをk分割した配列を返す（\[0:5::5] = [0,1.25,2.5,3.75,5]）
  
○\[i:j:k] （内包表記）for(int I = i;I<k;I+=k) で得られるIから成る配列と同じ。kは自動で符号逆になったりする

○[式 for 変数 : 条件 : 式]（内包表記）
     
○[式 foreach 変数 in index if 条件]（内包表記）
     
○lambda 変数 : 式　（ラムダ式） 
     
○x = y（代入）
     
○x ○= y類

*#

