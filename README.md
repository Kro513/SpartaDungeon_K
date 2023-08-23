# SpartaDungeon_K
using System.Reflection.PortableExecutable;
using System.Xml.Linq;
using System;
using System.Text;
using System.Net.Http.Headers;

namespace SpartaDungeon
{
    internal class Program
    {
        private static Character player;
        
        private static Item IronArmor;
        private static Item OldSword;


		static void Main(string[] args)
        {
            GameDataSetting();
            DisplayGameIntro();
        }

        static void GameDataSetting()
        {
            //캐릭터 정보
            player = new Character("Chad", "전사", 1, 10, 5, 100, 1500);

			//아이템 정보
			IronArmor = new Item("무쇠갑옷", 0, 5 ,"무쇠로 만들어져 튼튼한 갑옷입니다.");
			OldSword = new Item("낡은 검", 2, 0, "쉽게 볼 수 있는 낡은 검 입니다.");
        }

        //인트로 화면
        static void DisplayGameIntro()
        {
            Console.Clear();

            Console.WriteLine("스파르타 마을에 오신 여러분 환영합니다.");
            Console.WriteLine("이곳에서 던전으로 들어가기 전 활동을 할 수 있습니다.");
            Console.WriteLine();
            Console.WriteLine("1. 상태 보기");
            Console.WriteLine("2. 인벤토리");
            Console.WriteLine();
            Console.WriteLine("원하시는 행동을 입력해주세요.");

            int input = CheckValidInput(1, 2);
            switch (input)
            {
                case 1:
                    DisplayMyInfo();
                    break;

                case 2:
                    DisplayInventory();
                    break;
            }
        }

        //상태창
        static void DisplayMyInfo()
        {
            Console.WriteLine("상태 보기");
            Console.WriteLine("캐릭터의 정보가 표시됩니다.");
            Console.WriteLine();
            Console.WriteLine($"LV.{player.Level}");
            Console.WriteLine($"{player.Name}({player.Job})");
            Console.WriteLine($"공격력 : {player.Atk} (장비공격력)");
            Console.WriteLine($"방어력 : {player.Def} (장비방어력)");
            Console.WriteLine($"체  력 : {player.Hp}");
            Console.WriteLine($"Gold : {player.Gold}G");
            Console.WriteLine();
            Console.WriteLine("0. 나가기");
            Console.WriteLine();
            Console.WriteLine("원하시는 행동을 입력해주세요.");

            int input = CheckValidInput(0, 0);
            switch (input)
            {
                case 0:
                    DisplayGameIntro();
                    break;
            }
        }

        //인벤토리
        static void DisplayInventory()
        {
            Console.WriteLine("인벤토리");
            Console.WriteLine("보유 중인 아이템을 관리할 수 있습니다.");
            Console.WriteLine();
            Console.WriteLine("[아이템 목록]");
            Console.WriteLine($"- {Equip}{IronArmor.Name} | 방어력 +{IronArmor.Def} | {IronArmor.Exp}");
            Console.WriteLine($"- {Equip}{OldSword.Name} | 공격력 +{OldSword.Atk} | {OldSword.Exp}");
            Console.WriteLine();
            Console.WriteLine("1. 장착 관리");
            Console.WriteLine("0, 나가기");
            Console.WriteLine();
            Console.WriteLine("원하시는 행동을 입력해주세요.");

            int input = CheckValidInput(0, 1);
            switch (input)
            {
                case 0:
                    DisplayGameIntro();
                    break;
                case 1:
                    InstallItem();
                    break;
            }
        }

       //장착관리 페이지
        static void InstallItem()
        {
            Console.WriteLine("인벤토리 - 장착 관리");
            Console.WriteLine("보유 중인 아이템을 장착할 수 있습니다.");
            Console.WriteLine();
            Console.WriteLine("[아이템 목록]");
			Console.WriteLine($"-1{Equip.Ox}{IronArmor.Name} | 방어력 +{IronArmor.Def} | {IronArmor.Exp}");
			Console.WriteLine($"-2{Equip.Ox}{OldSword.Name} | 공격력 +{OldSword.Atk} | {OldSword.Exp}");
			Console.WriteLine();
            Console.WriteLine("0, 나가기");
            Console.WriteLine();
            Console.WriteLine("원하시는 행동을 입력해주세요.");

			int input = CheckValidInput(0, 2);
			switch (input)
			{
				case 0:
					DisplayInventory();
					break;
                case 1:
                    Equip();
                    break;
                case 2:
                    Equip();
                    break;
			}
		}

       

        //입력값 받을 때
        static int CheckValidInput(int min, int max)
        {
            while (true)
            {
				string? input = Console.ReadLine();

                bool parseSuccess = int.TryParse(input, out var ret);
                if (parseSuccess)
                {
                    if (ret >= min && ret <= max)
                        return ret;
                }

                Console.WriteLine("잘못된 입력입니다.");
            }
        }

        
    }

	//장비착용 함수에 한번 선택할때마다 -1을 곱해주어 음수와 양수로 착용 여부를 구분할 수 있도록 만들고싶음.
    public void Equip()
	{
		string Ox;
		int equip = 1;
        equip *= -1;


		if (equip > 0)
		{
			Ox = "[E]";
		}
		else
		{
			Ox = "";
		}
	}

	//캐릭터 클래스
    public class Character
    {
        public string Name { get; }
        public string Job { get; }
        public int Level { get; }
        public int Atk { get; }
        public int Def { get; }
        public int Hp { get; }
        public int Gold { get; }

        public Character(string name, string job, int level, int atk, int def, int hp, int gold)
        {
            Name = name;
            Job = job;
            Level = level;
            Atk = atk;
            Def = def; 
            Hp = hp;
            Gold = gold;
        }
    }

    //아이템 클래스
    public class Item
    {
        public string Name { get; }
        public int Atk { get; }
        public int Def { get; }
        public string Exp { get; }

        public Item(string name, int atk, int def, string exp)
        {
            Name = name;
            Atk = atk;
            Def = def;
            Exp = exp;
        }
    }

    //아이템 클래스 상속받은 무쇠갑옷
    public class IronArmor : Item
    {
		public IronArmor(string name, int atk, int def, string exp) : base(name, atk, def, exp)
		{
		}
    }
	//아이템 클래스 상속받은 낡은 검
	public class OldSword : Item
    {
		public OldSword(string name, int atk, int def, string exp) : base(name, atk, def, exp)
		{
		}
    }
	
}
