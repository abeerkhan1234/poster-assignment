using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApplication12
{
    public class Player
    {
        public int Strength
        {
            get;
            set;
        }
        public List<int> Opponents
        {
            get;
            private set;
        }
        public Player()
        {
            Opponents = new List<int>();
        }
        // Return winner of the match and remember opponent
        // O(1)
        static Player Play(Player p1, Player p2)
        {
            if (p1.Strength > p2.Strength)
            {
                p1.Opponents.Add(p2.Strength);
                return p1;
            }
            p2.Opponents.Add(p1.Strength);
            return p2;
        }

        // Runtime O(n) + O(logn)
        static void Main(string[] args)
        {
            // Test data setup, even number list
            var playerStrengths = new[] { 1, 2, 5, 4, 9, 7, 8, 7, 5, 4, 1, 0, 1, 4, 2, 3 };
            var players = playerStrengths.Select(i => new Player { Strength = i }).ToList();
            Console.WriteLine("Participants:\n");
            for (int j=0; j<16; j++)
            {
                
                Console.WriteLine("Player {0} = {1} ",j,playerStrengths[j]);
            }

            // O(n)
            while (players.Count > 1)
            {
                    var nextRound = new List<Player>();
                    for (int i = 0; i < players.Count - 1; i += 2)
                    {
                        Player winner = Play(players[i], players[i + 1]);
                        nextRound.Add(winner); // add winner of the match
                    }
                    players = nextRound;

            }
          

            // O(1)
            var tournamentWinner = players.First();
            int first = tournamentWinner.Strength;
            int second = -1;

            // O(logn)            
            foreach (int i in tournamentWinner.Opponents)
                if (i > second)// update                
                    second = i;
            
            Console.WriteLine("\nFirst Place: {0}, Second Place: {1}", first, second);
            Console.WriteLine("press key...");
            Console.ReadKey();
        }

    }
}
