# prog6112exam
Exam
Question1
public class Question1main {

public static void main(String[] args) {

        // A one-dimensional array stores the Month and products for the report.
        String[] products = {"Cozy Nights Mornarch mattress", "Restonic Bardos Mattress", "Sealy Phuket mattress"};
        String[] months = {"Month 1", "Month 2","Month 3"};

        // A two-dimensional array stores each year's sales by month.
        int[][] monthlySales = {
            {25, 18, 20}, 
            {15, 10, 12},
            {18, 15, 20}
        };

        // Create the calculation class and obtain the report values.
        ProductSalesReport report = new ProductSalesReport();

        System.out.println("========================================");
        System.out.println("       PRODUCTS SOLD REPORT");
        System.out.println("========================================");

        // Display the original SALES data.
        System.out.printf("%-12s %-10s %-10s %-10s%n",
                "Month", products[0],
                products[1], products[2]);

        for (int row = 0; row < monthlySales.length; row++) {
            System.out.printf("%-12s", "Month " + (row + 1));

            // Display each Product sales for this month.
            for (int value : monthlySales[row]) {
                System.out.printf("%-10d", value);
            }
            System.out.println();
        }

        // Display the calculated report.
        System.out.println("----------------------------------------");
        System.out.println("Total ProductSold: " + report.calculateTotal(monthlySales));
        System.out.printf("Average Bookings: %.2f%n", report.calculateAverage(monthlySales));
        System.out.println("Highest Bookings: " + report.calculateHighest(monthlySales));
        System.out.println("Most popular product: " + report.calculateHighest(monthlySales));
        System.out.println("========================================");
    }
}

Question 2
public class ProductSales implements IProductSales {

    // The examination specifies a sales limit of 500.
    public static final int SALES_LIMIT = 500;

    // Rows represent years; columns represent microphone, speakers and mixing desk.
    private final int[][] productSales = {
            {25, 18, 20}, 
            {15, 10, 12},
            {18, 15, 20}
    };

    /**
     * Returns a copy of the sales array so callers cannot change the original data.
     */
    @Override
    public int[][] GetProductSales() {
        int[][] copy = new int[productSales.length][];

        // Copy each row separately to protect the internal array.
        for (int row = 0; row < productSales.length; row++) {
            copy[row] = productSales[row].clone();
        }
        return copy;
    }

    /**
     * Calculates the total sales for all years and products.
     */
    @Override
    public int GetTotalSales() {
        int total = 0;

        // Add every product's sales for every month.
        for (int[] month : productSales) {
            for (int sale : month) {
                total += sale;
            }
        }
        return total;
    }

    /**
     * Counts sales values that are greater than the sales limit.
     */
    @Override
    public int GetSalesOverLimit() {
        int count = 0;

        // A sale equal to 500 is not over the limit.
        for (int[] month : productSales) {
            for (int sale : month) {
                if (sale > SALES_LIMIT) {
                    count++;
                }
            }
        }
        return count;
    }

    /**
     * Counts sales values that are lower than the sales limit.
     */
    @Override
    public int GetSalesUnderLimit() {
        int count = 0;

        // A sale equal to 500 is not under the limit.
        for (int[] month : productSales) {
            for (int sale : month) {
                if (sale < SALES_LIMIT) {
                    count++;
                }
            }
        }
        return count;
    }

    /**
     * Returns the number of years processed in the sales array.
     */
    @Override
    public int GetProductsProcessed() {
        return productSales.length;
    }

    /**
     * Calculates the average sales value across all products and years.
     */
    @Override
    public double GetAverageSales() {
        int numberOfSales = 0;

        // Count each sales entry in the array.
        for (int[] year : productSales) {
            numberOfSales += year.length;
        }

        return (double) GetTotalSales() / numberOfSales;
    }
}

