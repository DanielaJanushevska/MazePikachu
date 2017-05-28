#**Maze Pikachu**

Windows Forms Project by: 
Boris Dedejski,Daniela Janushevska

[1-*Македонски]

##1. Опис на апликацијата

Апликацијата што ја развивавме е класична игра Лавиринт во која од стартната позиција треба да се стигне до целта.
Со движење на маусот го движите курсорот(пикачу) така што избегнувајки ги препреките и стапиците(обележани со 
костур),пред да истече времето(timerot) којшто е 1 минута, и пред да ги изгубите животите (10 на број) треба да стигнете до целта. При тоа исто така треба да соберете што е можно повеќе овошја.На почетокот имате 10 животи со секое удирање во препрека или во паѓање во стапица тогаш животите ви се намалуваат а курсорот(пикачу) ви се враќа на стартната позиција. Доколку ги изгубите сите животи ви се отвара почетното мени за дали сакате играта да ја играте повторно или да ја исклучите.

![Alt text](Screenshots/Start.jpg?raw=true "Start the Game")

![Alt text](Screenshots/Maze.jpg?raw=true "MazePikachu")

##2.Упатство за Користење

#2.1 Копче START

Со цел да обезбедиме комплетно задоволство кај играчот креиравме чист и едноставен дизајн за да може да ја игра и разбира секој па така со кликнување на копчето START играта започнува (се отвара во нов прозорец),TIMEROT почнува да брои,ако ви истече времето (TIMEROT) ве враќа на почетното МЕНИ со цел да одберете дали сакате играта да ја играте повторно или да завршите.
Целта на играта е да ги поминете препреките, да ги избегнете стапиците(обележани со костур) и да соберете што е можно повеќе овошја и да стигнете до жолтото знаме (до FINISH-от). Повеќе овошја ви носат повеќе поени.
На почеток имате на располагање 10 животи (LIVES) ако допрете во некоја препрека или сте во стапица тогаш ве враќа на почетната позиција а бројот на живот ви се намалува и ако ги изгубите сите животи а не стигните до целта ви се отвара повторно почетното мени да изберете дали повторно ке ја играте играта.

![Alt text](Screenshots/Win.jpg?raw=true "Win")

![Alt text](Screenshots/Lose.jpg?raw=true "Lose")

#2.2 Копче QUIT

Со кликнување на копчето QUIT до менито се гаси играта.

#2.3 Правила

#Правилата се едноставни 

* Пожелно е  да соберете што е можно повеќе овошја
* Не смеете да ги изгубите животите ако сакате да стигнете до целта
* Пред да истече времето треба да стигнете до целта 


##3. Претставување на проблемот

###3.1 Податочни структури

Главните податоци и [функции]за играта се чуваат во класа ```public partial class Form1 : Form```
Препреките,овошјата,стапиците, и трепкачките препреки ни се претставени со лабели.
Со оваа класа ja дефинираме играта т.е. ги дефиниравме препреките,курсорот,овошјата,стапиците,финишот,тајмерот,животите...

За која форма прва ќе се отвара во Program.cs  
Application.Run(new Start()); со кое Start ни е класата за почетната форма на која излегува менито.
Класата Start e многу едноставна има 2 копчиња и тие се: START(кое не носи на играта FORM1) и QUIT (кое не гаси од играта FORM1 или со име Maze Pikachu).
Таму ги имаме функциите :
private void button1_Click(object sender, System.EventArgs e)
        {
            Form1 frm = new Form1();
            frm.Show();
            this.Hide();
            
        }
        private void button2_Click(object sender, System.EventArgs e)
        {
            Form1 frm = new Form1();
            frm.Close();
            this.Hide();

        }
Kое со кликнување на button1 не префрла на Form1 со кликнување на button2 на тековната форма.


Во примарната класа: 
		public Form1()
        {
            InitializeComponent();
            Bitmap b = new Bitmap(Resources.emesprani172);
            this.Cursor = CustomCursor.CreateCursor(b, 17, 2);
            Point startingPoint = panel1.Location;
            startingPoint.Offset(10, 10);
            Cursor.Position = PointToScreen(startingPoint);
        }

ја дефиниравме позицијата на маусот кога ќе почне игратата на почетокот на панелот.

#3.2 Функции

	1) Функцијата (private void Finish_MouseEnter)
		е функција кога ке влеземе на жолтото поле FINISHOТ да ни испечати во порака дека ова е FINISH и дека победивме
		и притоа не враќа на почетната форма доколку сакаме уште еднаш да ја играме играта.
		
	2) Функцијата (private void MoveToStart())
        {
            Point startingPoint = panel1.Location;
            startingPoint.Offset(10, 10);
            Cursor.Position = PointToScreen(startingPoint);
        }
		се повикува секогаш кога ќе удриме во препрека или стапица на позицијата на маусот да е на стартна позиција.
	
	3)Функцијата (private void zid_MouseEnter(object sender, EventArgs e))
        {
            lives--;
            this.Refresh();
            if (lives == 0)
            {
                MessageBox.Show("GAME OVER!");
                Start frm = new Start();
                frm.Show();
                this.Hide();
            }
            MoveToStart();
        }
		ја користиме секогаш кога ќе удриме во препрека за да ни се намалат животите.
		Притоа ја повикуваме функцијата MoveToStart() којашто е изведена погоре за да не врати на стартна позиција.
		Ако животите се 0 ни се појавува порака "GAME OVER!", па се исклучува формата и се враќаме на стартна форма.
		
	4) Функцијата (private void timer1_Tick(object sender, EventArgs e))
	 Оваа функција ни е за трепкачките препреки(црвените линии кои трепкаат):
	 {
            if (flag == 0)
            {
                label29.Enabled = true;
                label29.Visible = true;
                label33.Enabled = true;
                label33.Visible = true;
                label32.Enabled = true;
                label32.Visible = true;
                label31.Enabled = true;
                label31.Visible = true;
                label40.Enabled = true;
                label40.Visible = true;
                flag = 1;

            }
            else
            {
                label29.Enabled = false;
                label29.Visible = false;
                label33.Enabled = false;
                label33.Visible = false;
                label32.Enabled = false;
                label32.Visible = false;
                label31.Enabled = false;
                label31.Visible = false;
                label40.Enabled = false;
                label40.Visible = false;
                flag = 0;
            }
        }
		Дефинираме едно знаме flag кое на почетокот е нула, ако flag e нула тогаш ни се видливи. На крај на функцијата го правиме flag=1.
		Во интервалот на timer1_Тick ја пишуваме брзината со која сакаме да трепкаат препреките. Нам ни се направени со 800 милисекунди.
		Доколку сакаме да трепкат побрзо ќе го намалиме интервалот.
		
	5) Функцијата private void label36_MouseEnter(object sender, EventArgs e)
			{
            fruits++;
            label36.Visible = false;
            this.Refresh();
			}
		Истото важи за функциите label38,label39,label41.
		Со овие лабели ни се претставени овошјата т.е. јаболката.
		Во MouseEnter на label38,label39,label41 ги повикуваме овие функции или тоа ни означува дека кога ќе поминеме со маусот низ лабелата ни се зголемува бројот на овошјата т.е. ни се одбројуваат. Автоматски се прави невидлива лабелата т.е. овошјето. Додека вредноста на променливата fruits ќе ја искористиме за да печатиме на екранот колку овошја сме собрале.
	
	6) Функција 
	    protected override void OnPaint(PaintEventArgs e)
        {
            Graphics dc = e.Graphics;
            TextFormatFlags flags = TextFormatFlags.Left;
            Font _font = new System.Drawing.Font("Stencil", 20, FontStyle.Bold);
            TextRenderer.DrawText(e.Graphics, "FRUITS 🍎: " + fruits.ToString(), _font, new Rectangle(678, 275, 200, 70), SystemColors.ControlText, flags);
            TextRenderer.DrawText(e.Graphics, "LIVES ❤️: " + lives.ToString(), _font, new Rectangle(678, 318, 200, 70), SystemColors.ControlText, flags);
            TextRenderer.DrawText(e.Graphics, "TIME LEFT ⏲️: " + timer2.ToString(), _font, new Rectangle(642, 12, 200, 70), SystemColors.ControlText, flags);
            base.OnPaint(e);
        }
		Со оваа функција ги печатиме вредноста на променливата Lives т.е. за да видиме колку животи ни преостанале на екран т.е. на позиција 678,318 со големина width:200 и height :70. Потоа користиме фонт Stencil со големина 20 BOLD. 
		Потоа ја печатиме вредноста на променливата Fruits т.е. за да видиме колку животи ни преостанале на екран т.е. на позиција 678,275 со големина width:200 и height :70. Користиме фонт Stencil со големина 20 BOLD. 
		Печатиме и колку време ни преостанува за да стигнеме до целта.
		
	7)  TIMER
		Тајмерот го имплементиравме со GIF(image) на button кој нема никаква фунцкија туку да одбројува 1 минута, со цел поубаво да ни одговара во дизајанот. Додека вредноста за да се гаси играта кога ќе заврши тајмерот го направивме со следната функција:
		private void timer2_Tick(object sender, EventArgs e)
        {
            Start frm = new Start();
            frm.Show();
            this.Hide();
            this.Close();
        }
		со која се гаси играта кога ке истече времето на овој тајмер. Вредноста на timerot ја сетиравме на Interval од 60000 милисекунди што е еднакво на 1 минута.
		
	8) Маусот во вид на слика го прикачивме со помошна класа CustomCursor.cs и CImageBase(каде што направивме BITMAP за    координати x i y) од кои ќе зимаме податоци кои ни се од помош за класата Form1.cs.
		Неговата слика ја ставивме преку Resources и ја именувавме како emesprani172.
		Така во главната класа на Form1() Bitmap b доаѓа од CImageBase.cs со нова Bitmapa која од Resources ни ја зима сликата па so this.Cursor(кој се однесува на тековниот курсор) од класата CustomCursor го зимаме методот CreadeCursor(со сликата од битмапата на б,na pozicija x=17 , pozicija y=2).
		
        public Form1()
        {
            InitializeComponent();
            Bitmap b = new Bitmap(Resources.emesprani172);
            this.Cursor = CustomCursor.CreateCursor(b, 17, 2); 

        }
		
		со тоа ја сменивме вредноста на курсорот од стрелка во слика (пикачу).

		
----------
[2* Еnglish]

##1. Descripiton of the game
This application is standard Maze game in which you need from the beginning to arrive to the End with the mouse movement 
then therefore escaping from the catches, before your time runs out and your lives are not spent.
You also need to get as much fruit as you can so your score can be even better.
To start the game you need to click on the Start button or to close the game you need to click Quit button.


##2.How to play
*Click Start
*Move the mouse till you reach the finish(yellow field)
*Do not get in catches, or your live will be spent and you will be back on the start position.
*Don't let your time runs out
*Collect as much fruits as you can. 


#License
This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

