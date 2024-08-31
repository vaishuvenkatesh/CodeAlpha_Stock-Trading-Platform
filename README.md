# CodeAlpha_Stock-Trading-Platform
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Scanner;

class Stock {
    private String symbol;
    private double price;

    public Stock(String symbol, double price) {
        this.symbol = symbol;
        this.price = price;
    }

    public String getSymbol() {
        return symbol;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        this.price = price;
    }
}

class Portfolio {
    private Map<String, Integer> holdings;
    private double cash;

    public Portfolio(double cash) {
        this.holdings = new HashMap<>();
        this.cash = cash;
    }

    public void buyStock(Stock stock, int quantity) {
        if (cash >= stock.getPrice() * quantity) {
            cash -= stock.getPrice() * quantity;
            holdings.put(stock.getSymbol(), holdings.getOrDefault(stock.getSymbol(), 0) + quantity);
            System.out.println("Bought " + quantity + " shares of " + stock.getSymbol());
        } else {
            System.out.println("Insufficient funds");
        }
    }

    public void sellStock(Stock stock, int quantity) {
        if (holdings.containsKey(stock.getSymbol()) && holdings.get(stock.getSymbol()) >= quantity) {
            cash += stock.getPrice() * quantity;
            holdings.put(stock.getSymbol(), holdings.get(stock.getSymbol()) - quantity);
            System.out.println("Sold " + quantity + " shares of " + stock.getSymbol());
        } else {
            System.out.println("Insufficient shares");
        }
    }

    public void displayHoldings() {
        System.out.println("Holdings:");
        for (Map.Entry<String, Integer> entry : holdings.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
        System.out.println("Cash: " + cash);
    }
}

public class StockTradingPlatform {
    private List<Stock> marketData;
    private Portfolio portfolio;
    private Scanner scanner;

    public StockTradingPlatform() {
        this.marketData = new ArrayList<>();
        this.portfolio = new Portfolio(10000);
        this.scanner = new Scanner(System.in);

        // Initialize market data
        marketData.add(new Stock("AAPL", 150));
        marketData.add(new Stock("GOOG", 2500));
        marketData.add(new Stock("MSFT", 200));
    }

    public void run() {
        while (true) {
            System.out.println("1. Display market data");
            System.out.println("2. Buy stock");
            System.out.println("3. Sell stock");
            System.out.println("4. Display portfolio");
            System.out.println("5. Exit");
            System.out.print("Choose an option: ");
            int option = scanner.nextInt();

            switch (option) {
                case 1:
                    displayMarketData();
                    break;
                case 2:
                    buyStock();
                    break;
                case 3:
                    sellStock();
                    break;
                case 4:
                    portfolio.displayHoldings();
                    break;
                case 5:
                    System.out.println("Exiting...");
                    return;
                default:
                    System.out.println("Invalid option. Please choose again.");
            }
        }
    }

    private void displayMarketData() {
        System.out.println("Market Data:");
        for (Stock stock : marketData) {
            System.out.println(stock.getSymbol() + ": " + stock.getPrice());
        }
    }

    private void buyStock() {
        System.out.print("Enter stock symbol: ");
        String symbol = scanner.next();
        System.out.print("Enter quantity: ");
        int quantity = scanner.nextInt();

        for (Stock stock : marketData) {
            if (stock.getSymbol().equals(symbol)) {
                portfolio.buyStock(stock, quantity);
                return;
            }
        }
        System.out.println("Invalid stock symbol");
    }

    private void sellStock() {
        System.out.print("Enter stock symbol: ");
        String symbol = scanner.next();
        System.out.print("Enter quantity: ");
        int quantity = scanner.nextInt();

        for (Stock stock : marketData) {
            if (stock.getSymbol().equals(symbol)) {
                portfolio.sellStock(stock, quantity);
                return;
            }
        }
        System.out.println("Invalid stock symbol");
    }

    public static void main(String[] args) {
        StockTradingPlatform platform = new StockTradingPlatform();
        platform.run();
    }
}
//OUTPUT
1. Display market data
2. Buy stock
3. Sell stock
4. Display portfolio
5. Exit
Choose an option: 1
Market Data:
AAPL: 150.0
GOOG: 2500.0
MSFT: 200.0

1. Display market data
2. Buy stock
3. Sell stock
4. Display portfolio
5. Exit
Choose an option: 2
Enter stock symbol: AAPL
Enter quantity: 10
Bought 10 shares of AAPL

1. Display market data
2. Buy stock
3. Sell stock
4. Display portfolio
5. Exit
Choose an option: 4
Holdings:
AAPL: 10
Cash: 9850.0

1. Display market data
2. Buy stock
3. Sell stock
4. Display portfolio
5. Exit
Choose an option: 3
Enter stock symbol: AAPL
Enter quantity: 5
Sold 5 shares of AAPL

1. Display market data
2. Buy stock
3. Sell stock
4. Display portfolio
5. Exit
Choose an option: 4
Holdings:
AAPL: 5
Cash: 9925.0

1. Display market data
2. Buy stock
3. Sell stock
4. Display portfolio
5. Exit
Choose an option: 5
Exiting...

# CodeAlpha_Stock-Trading-Platform
