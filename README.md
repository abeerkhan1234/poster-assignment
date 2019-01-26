using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApplication12
{
    public class Program
    {

        static Random _rnd = new Random();

        static int[] Generate(int n)
        {

            int[] a = new int[n];

            for (int i = 0; i < n; i++)
                a[i] = _rnd.Next(100);

            return a;

        }

        static void TwoSmallestValues(int[] a, out int min1, out int min2)
        {

            min1 = a[0];
            min2 = a[1];
            if (min2 < min1)
            {
                min1 = a[1];
                min2 = a[0];
            }

            for (int i = 2; i < a.Length; i++)
                if (a[i] < min1)
                {
                    min2 = min1;
                    min1 = a[i];
                }
                else if (a[i] < min2)
                {
                    min2 = a[i];
                }

        }

        static void Main(string[] args)
        {

            while (true)
            {

                Console.Write("n=");
                int n = int.Parse(Console.ReadLine());

                if (n < 2)
                    break;

                int[] a = Generate(n);

                int min1, min2;

                TwoSmallestValues(a, out min1, out min2);

                Console.Write("{0,4} and {1,4} are smallest in:", min1, min2);
                for (int i = 0; i < a.Length; i++)
                    Console.Write("{0,4}", a[i]);
                Console.WriteLine();
                Console.WriteLine();

            }

            Console.Write("Press ENTER to continue... ");
            Console.ReadLine();

        }
    }
}
