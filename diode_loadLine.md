# 다이오드 Load Line 그리는법

> 아래 자료는 제주대학 전자회로 강의자료입니다!
> 
>  제가 직접 만들었고 저작권은 저에게 있습니다!

## 목차

1. [기초적인 회로 구성법](#1-기초적인-회로-구성법)
2. [시뮬설정방법](#2-시뮬설정방법)
3. [X축 다이오드 전압으로 바꾸기](#3-x축-다이오드-전압으로-바꾸기)
4. [diode 그래프 표시하기](#4-diode-그래프-표시하기)
5. [Load Line 구하기 이론](#5-load-line-구하기-이론)
6. [Pspice에서 Load Line 출력](#6-pspice에서-load-line-출력)
---

# 1 기초적인 회로 구성법

![01](/picture/01.png)

먼저 Pspice로 위와 같은 회로를 구상한다.



![02](/picture/02.png)

참고로 D1N4001은 정류 다이오드 이다.

![03](/picture/03.jpg)

Place에 netAlias를 클릭한다.

![04](/picture/04.jpg)

Alias는 D로 설정한다.

![05](/picture/05.jpg)

Alias를 위 그림과 같은 위치에 놓는다.

---

# 2 시뮬설정방법

![06](/picture/06.jpg)

상단 메뉴에서 New Simulation Profile을 클릭한다.

![07](/picture/07.jpg)

1. 먼저 Analysis Type을 DC Sweep으로 바꾼다.
2. Voltage Source의 Name을 V1으로 바꾼다.
3. Stare Value를 0V End Value를 5V로 설정한다.(이때 increment가 작을 수록 정밀도가 커진다.)
4. OK버튼을 누른다.

![08](/picture/08.jpg)

Run Pspice를 클릭한다.

---

# 3 X축 다이오드 전압으로 바꾸기
### 기존에는 Source의 V로 설정되어 있었기 때문에 이를 수정하는 과정이 필요하다.

![09](/picture/09.jpg)

우클릭을 누른후 Settings에 들어간다.

![10](/picture/10.jpg)

Axis Variable에 들어간다.

![11](/picture/11.jpg)

V(D)로 설정하고 OK를 눌러준다.

![12](/picture/12.jpg)

아래의 값이 V(D)로 바뀌면서 단위가 바뀐것을 확인할 수 있다.

---

# 4 diode 그래프 표시하기

![13](/picture/13.jpg)

우클릭후 AddTrace를 클릭한다.

![14](/picture/14.jpg)

I(D1)값을 넣어준다.

![15](/picture/15.jpg)

그래프가 잘 출력되는 것을 확인 할 수 있다.

---

# 5 Load Line 구하기 이론

<img src="/picture/17.jpg" width="300" height="150">

다음 회로는
KVL법칙에 따라 아래와 같은 식이 나온다.

$$
V_{DD}-I_{D}R_{L}-V_{D}=0
$$

$$
V_{DD}=I_{D}R_{L}+V_{D}. . . 1
$$

$$
when \ \ \ V_{DD}=0 -> I_{D}=\frac{V}{R_{L}}
$$

$$
when \ \ \ I_{D}=0 -> V_{D}=V_{DD}
$$

따라서 Load Line은 다음과 같다.

<img src="/picture/16.jpg" width="500" height="350">

여기서 VDD는 최대 5V이고 RL은 100Ω이므로 

$$V_{DD}=5V$$

$$\frac{V_{DD}}{R}=\frac{5V}{100Ω}=50mA$$

x절편 = $5V$
y절편 = $50mA$

$$
\begin{align}
& y=-\frac{50mA}{5V}(V_{D}-5V) \\
&\implies-10m℧*V_{D}+50mA
\end{align}
$$

---

# 6 Pspice에서 Load Line 출력

![18](/picture/18.jpg)

Add Trace를 클릭한다.

![19](/picture/19.jpg)

-(10e-3)*V(D)+50e-3을 입력해준다.
>$$
\begin{align}
& y=-\frac{50mA}{5V}(V_{D}-5V) \\
&\implies-10m℧*V_{D}+50mA
\end{align}
$$
>


![20](/picture/20.jpg)

Load Line이 잘 출력되는 것을 확인 할 수 있다.
여기서 diode response그래프와 Load Line이 만나는 지점이 Q포인트가 된다.
