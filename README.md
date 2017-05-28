#**Maze Pikachu**

Windows Forms Project by: 
Boris Dedejski,Daniela Janushevska
[1-*Македонски]

##1. Опис на апликацијата
Апликацијата што ја развивавме е класична игра Лавиринт во која од стартната позиција треба да се стигне до целта.
Со движење на маусот го движите курсорот(човечето) така што избегнувајки ги препреките избегнувајки ги стапиците(обележани со 
костур) 
,пред да истече 
времето(timerot)што е 1 минута,и пред да ги изгубите животите треба да стигните до целта.При тоа исто така треба да соберете што е можно повеќе 
овошја.На почетокот имате 10 животи со секое удирање во препрека или во паѓање во стапица тогаш животите ви се намалуваат
а курсорот(човечето) ви се враќа на стартната позиција.Доколку ги изгубите сите животи ви се отвара почетото мени за дали сакате
играта да ја играте повторно или да исклучите.

##2.Упатство за Користење
#2.1 Копче START
Со цел да обезбедиме комплетно задоволство кај играчот креиравме чист и едноставен дизајн за да може да ја игра и разбира секој
Така со кликнување на копчето START играта започнува (се отвара во нов прозорец),TIMEROT почнува да брои,ако ви истече времето (TIMEROT)ве враќа на почетното МЕНИ
со цел да одберете дали сакате играта да ја играте повторно или да завршите.
Целта на играта е да ги изммините препреките да ги избегнете стапиците(обележани со костур) и да зберете што е можно повеќе овошја и да стигнете до жолтото знаме (до FINISH-от)
Повеќе овошја ви носат повеќе поени.
На почеток имате на располагање 10 животи (LIVES) ако удрите во некоја препрека или сте во стапица тогаш ве враќа на почетната позиција 
а бројот на живот ви се намалува ако ги изгубите сите животи а не стигните до целта ви се отвара повторно почетното мени да изберете дали повторно ке ја 
играте играта

#2.2 Копче QUIT

Со кликнување на копчето QUIT до менито се гаси играта.
#2.3 Правила
#Правилата се едноставни 

* Треба да соберете што е можно повеќе овошја за да имате подобар score
* Не смеете да ги изгубите животите ако сакате да стигните до целта
* Пред да истече времето треба да стигните до целта 


##3. Претставување на проблемот

###3.1 Податочни структури
Главните податоци и [функции]за играта се чуваат во класа ```    public partial class Form1 : Form
```
Препреките,овошјата,стапиците, и трепкачките препреки ни се претставени со лабели.
Со оваа класа ja дефинираме играта ги дефиниравме препреките,курсорот,овошјата,стапиците,финишот,тимерот,животите,

За која форма прва ке се отвара во Program.cs             
Application.Run(new Start()); со кое Start ни е класата за почетната форма на која излегува менито

Класата Start e многу едноставна има 2 копчиња START(кое не носи на играта FORM1) и QUIT (кое не гаси од играта FORM1)
Таму ги имаме функциите 
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
кое со кликнување на button1 не префрла на form1 so Клукнување на button2 ја тековната форма.




Во примарната класа 
		public Form1()
        {
            InitializeComponent();
            Bitmap b = new Bitmap(Resources.emesprani172);
            this.Cursor = CustomCursor.CreateCursor(b, 17, 2);
            Point startingPoint = panel1.Location;
            startingPoint.Offset(10, 10);
            Cursor.Position = PointToScreen(startingPoint);

        }

ја дефиниравме позицијата на маусот кога ке почне игратата на почетокот на панелот.

#3.2 Функции
	1)	функцијата (private void Finish_MouseEnter)
		е функција кога ке флеземе на жолтото поле FINISHOТ да ни испечати во порака дека ова е FINISH и дека поведивме
		и притоа не вракаќа на полетната форма доколку сакаме уште еднаш да ја играме играта
		
	2) функцијата (private void MoveToStart())
        {
            Point startingPoint = panel1.Location;
            startingPoint.Offset(10, 10);
            Cursor.Position = PointToScreen(startingPoint);
        }
		се повикува секогаш кога ке удриме во препрека или стапица позицијата на куросорт да е на стартна позиција
	
	3)функцијата  (private void zid_MouseEnter(object sender, EventArgs e))
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
		ја користиме секогаш кога ке удриме во препрека да ни се намалат животите.
		Притоа ја повикуваме фунцкијата MoveToStart() изведена погоре за да не врати на стартна позиција.
		Ако животите се 0 ја гасиме играта се враќаме на стартна форма и пишуваме GAME OVER
		
	4)функција    (private void timer1_Tick(object sender, EventArgs e))
	 Оваа Фунцкија ни е за трепкачките препреки(црвените кои трепкаат)
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
		Оваа Фунцкија ни е за трепкачките препреки(црвените кои трепкаат)
		Дефинираме едно знаме flag кое на почеток е нула ако flag e нула тогаш ни се видливи 
		на крај на фунцкијата го правиме flag=1 за да следниот пат кога тимерот ке чукне препреките да не ни
		се видливи
		Во интервалот на timer1_Тick ја пишуваме брзината со која сакаме да трепкаат препреките.Нам ни се направени со 800 милисекунди
		Доколку сакаме да трепкат побрзо ќе го намалиме интервалот.
		
	5)Фунцкија private void label36_MouseEnter(object sender, EventArgs e)
			{
            fruits++;
            label36.Visible = false;
            this.Refresh();
			}
		Истото важи за фунцкиите label38,label39,label41
		Со овие лабели ни се претставени овошјата јаболните
		Во MouseEnter на label38,label39,label41 ги повикуваме овие функции
		или тоа ни означува кога ке поминеме со маусот низ оваа лабела(овошјата)
		овошјата ни се зголемуваат,Ја правиме невидлива лабелата(овошјето)
		(вредноста на променливата fruits ќе ја искористиме за да печатиме на екранот колку овошја сме собрале)
	
	
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
		Со оваа функција ги печатиме вредноста на променливата Lives(за да видиме колку животи ни преостанале на екран)на позиција 678,318 со големина 
		width:200 и height :70 Со фонт Stencil со големина 20 BOLDирано 
		ги печатиме вредноста на променливата Fruits(за да видиме колку животи ни преостанале на екран)на позиција 678,275 со големина 
		width:200 и height :70 Со фонт Stencil со големина 20 BOLDирано 
		Печатиме и колку време ни преостанува за да стигнеме до целта.
	
	
	7) ТИМЕР
		Тимерот го имплементиравме со GIF(image) на button кој нема никаква фунцкија туку да одбројува 1 минута со цел поубаво да ни одговара во дизјанот
		а вредноста за да се гаси играта кога ке заврши тајмерот го направивме со функцијата
		private void timer2_Tick(object sender, EventArgs e)
        {
            Start frm = new Start();
            frm.Show();
            this.Hide();
            this.Close();
        }
		со која се гаси играта кога ке истече овој timer.Вредноста на timerot ја сетиравме на Interval од 60000 милисекунди што е еднакво на 1 миута
	
	
	8) Куросрот во вид на слика го прикачивме со помошна класа CustomCursor.cs и CImageBase(каде што направивме BITMAP за координати x i y) од кои ке зимаме податоци кои ни се од
		помош за класата Form1.cs
		неговата слика ја ставивме преку Resources и ја именувавме како emesprani172
		така во главната класа на Form1() 
		Bitmap b доаѓа од CImageBase.cs со нова Bitmapa која од Resources ни ја зима сликата
		па so this.Cursor(кој се однесува на тековниот курор) од калсата CustomCursor го зимаме методот CreadeCursor(со сликата од битмапата на б,na pozicija x=17 , pozicija y=2)
		
        public Form1()
        {
            InitializeComponent();
            Bitmap b = new Bitmap(Resources.emesprani172);
            this.Cursor = CustomCursor.CreateCursor(b, 17, 2); 

        }
		
		со тоа ја сменивме вредноста на курсорот од стрелка во слика (човече)

		
----------
[2* Еnglish]

##1. Descripiton of the game
This application is standard Maze game in which you need from the beginning to arrive to the End with the mouse movement 
then therefore escaping from the catches,before your time runs out and your lives are not spent.
You also need to get as much fruit as can so your score can be even better.
To start the game you need to click on the Start button or to finish the game you need to click Quit button.


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

