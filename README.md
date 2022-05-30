/* 実装型
int
double

ivec2(x,y)
dvec2(x,y) 2次元ベクトル

hsva(h,s,v,a)
rgba(r,g,b,a) 色

Sprite　スプライト定義

Player 自機
PB 自機の弾
PL 自機のレーザー

Effect エフェクト

Bullet 弾 
LaserA レーザーA（まっすぐ）
LaserB レーザーB（直線）
LaserC レーザーC（へにょり）

BulletManager 弾の一括処理用

Enemy 敵
Boss  ボス

配列 例：int[6]


*/
/* 定数、関数のメモ

弾

clone そのまま複製

vertical　1なら斜め45度になる

way　　　　角度と個数

radial　　円

line　　　速度だけバラバラ

winder　　時間をずらす


移動用

moveabs(r,v)

moverel(r,v)

move2abs(r,f)

move2rel(r,f)

move3abs(r,v0,v1)

move3rel(r,v0,v1)

move4abs(r,r1,r2,f)

move4rel(r,r1,r2,f)


ランダム
irand(i,j)

drand(x,y)

srand() : -1か1

数学関数
max(...),min(...),clamp(...)

ceil(x),floor(x)

sgn(x),abs(x) :sgnはvec2の偏角、absはvec2の長さとしても使える

sin(x),cos(x),tan(x)

sinh(x),cosh(x),tanh(x)

asin(x),acos(x),atan(x)

asinh(x),acosh(x),atanh(x)

exp(x),ln(x),lb(x),lg(x),log(x,a)

*/
/* stat 文のメモ

文;文
文（改行）文

宣言 例：int x = 0
式　　例：x = 1+2 sin(4)

if文 if 式:
     elif 式:
     else:
     switch 式:
     case 値:
     ....
     default:
     ....

while文 while 式:
for文   for 変数 : 式 : 式:
foreach文　 foreach i in index:

break文、continue文、pass文

return文 return
yield文 yield

wait文　wait(n) = yieldをn回

when文 when 式:　トリガー用。trueになったら式を実行する

class文 class(コンストラクタ用変数) :上位クラス

*/

/*exp：演算子のメモ

○x.m<t> : tフレーム後の値
使うたびにデータ更新（v.x<3> *= 15 →wait(15) v.x *= 15という中身のスレッドを立てる ）
値として使う場合

omega<t> : 最も近い過去のomegaのまんま
a<t> : 最も近い過去のaを基準に、v,a,omegaから計算 a<T+1> = a<T>@omega<T>
v<t> : 最も近い過去のvを基準に、v,a,omegaから計算 v<T+1> =(v<T>+a<T>)@omega<T> から計算
r<t> : 最も近い過去のrを基準に、r,v,a,omegaから計算 r<T+1> = r<T> + v<T>

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

○type(x)

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
if ~ :系とは、:の次が改行かどうかで判断

配列操作式

○[式 foreach 変数 in index if 条件]（内包表記）
○lambda a,b : a*b　（ラムダ式） 
○x = y（代入）
○x ○= y類

*/
