using System;

class Money
{
    private int rubles; 
    private int kopeck; 


    public Money(int rubles, int kopeck)
    {
        this.rubles = rubles;
        this.kopeck = kopeck;
        Normalize(); 
    }

    
    private void Normalize()
    {
        if (kopeck >= 100)
        {
            rubles += kopeck / 100;
            kopeck = kopeck % 100;
        }
        if (kopeck < 0)
        {
            rubles -= 1;
            kopeck += 100;
        }
        if (rubles < 0 && kopeck > 0)
        {
            rubles += 1;
            kopeck -= 100;
        }
    }

    
    public Money Add(Money other)
    {
        int newRubles = this.rubles + other.rubles;
        int newKopeck = this.kopeck + other.kopeck;
        return new Money(newRubles, newKopeck);
    }

    
    public Money Subtract(Money other)
    {
        int newRubles = this.rubles - other.rubles;
        int newKopeck = this.kopeck - other.kopeck;
        return new Money(newRubles, newKopeck);
    }

    
    public Money Multiply(double factor)
    {
        double totalKopecks = (rubles * 100 + kopeck) * factor;
        int newRubles = (int)(totalKopecks / 100);
        int newKopeck = (int)(totalKopecks % 100);
        return new Money(newRubles, newKopeck);
    }

   
    public Money Divide(double divisor)
    {
        if (divisor == 0)
        {
            Console.WriteLine("Ошибка: деление на 0!");
            return new Money(0, 0);
        }
        double totalKopecks = (rubles * 100 + kopeck) / divisor;
        int newRubles = (int)(totalKopecks / 100);
        int newKopeck = (int)(totalKopecks % 100);
        return new Money(newRubles, newKopeck);
    }

   
    public void Increment()
    {
        kopeck++;
        Normalize();
    }

    
    public void Decrement()
    {
        kopeck--;
        Normalize();
    }

    
    public bool IsLessThan(Money other)
    {
        if (this.rubles < other.rubles)
            return true;
        if (this.rubles == other.rubles && this.kopeck < other.kopeck)
            return true;
        return false;
    }

    public bool IsGreaterThan(Money other)
    {
        if (this.rubles > other.rubles)
            return true;
        if (this.rubles == other.rubles && this.kopeck > other.kopeck)
            return true;
        return false;
    }

    public bool IsEqualTo(Money other)
    {
        return this.rubles == other.rubles && this.kopeck == other.kopeck;
    }

    
    public void Display()
    {
        Console.WriteLine($"{rubles} руб {kopeck} коп");
    }
}

class Program
{
    static void Main(string[] args)
    {
       
        Money money1 = new Money(10, 50); 
        Money money2 = new Money(5, 75);  

        Console.WriteLine("Первая сумма:");
        money1.Display();

        Console.WriteLine("Вторая сумма:");
        money2.Display();

        Console.WriteLine("Сложение:");
        Money sum = money1.Add(money2);
        sum.Display();

        Console.WriteLine("Вычитание:");
        Money diff = money1.Subtract(money2);
        diff.Display();

        Console.WriteLine("Умножение на 2:");
        Money mult = money1.Multiply(2);
        mult.Display();

        Console.WriteLine("Деление на 2:");
        Money div = money1.Divide(2);
        div.Display();

        Console.WriteLine("Увеличение на 1 копейку:");
        money1.Increment();
        money1.Display();

        Console.WriteLine("Уменьшение на 1 копейку:");
        money1.Decrement();
        money1.Display();

        Console.WriteLine("Сравнение (меньше): " + money1.IsLessThan(money2));
        Console.WriteLine("Сравнение (больше): " + money1.IsGreaterThan(money2));
        Console.WriteLine("Сравнение (равно): " + money1.IsEqualTo(money2));
    }
}
