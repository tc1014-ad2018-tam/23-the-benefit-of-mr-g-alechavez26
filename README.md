# 23-the-benefit-of-mr-g-alechavez26
23-the-benefit-of-mr-g-alechavez26 created by GitHub Classroom
/*This program can sell tickets to this show. The system must have an initial menu with the following options.
 * A. Sell a ticket.
 * B. Save sells data.
 * C. Reports.
 * D. Exit.
 *
 * Alejandra Chávez Cruz
 * A01411970@itesm.mx
 * 05/nov/18
 *
 */

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>

void MainMenu() {
    printf("\nHi.\n");
    printf("Choose an option:\n");
    printf("1. Buy a ticket.\n");
    printf("2. Save sells data.\n");
    printf("3. Reports.\n");
    printf("4. Exit.\n");
}

// Function to print the reports menu.
void ReportsMenu() {
    printf("Choose an option:\n");
    printf("1. Total tickets sold.\n");
    printf("2. Total tickets sold per zone.\n");
    printf("3. Total income.\n");
    printf("4. Total income per zone.\n");
    printf("5. Occupation rate.\n");
    printf("6. Occupation rate per zone.\n");
}

// Function to print the zones.
void Zones() {
    printf("Choose your zone:\n");
    printf("1. VIP: $100\n");
    printf("2. Platinum: $85\n");
    printf("3. Gold: $70\n");
    printf("4. Silver: $55\n");
    printf("5. Green: $45\n");
    printf("6. Yellow: $40\n");
    printf("7. Red: $30\n");
    printf("8. Sky Blue: $50\n");
    printf("9. Navy Blue: $35\n");
    printf("10. Deep Blue: $20\n");
}

// Function to print the payment methods.
void PayementMethod() {
    printf("Choose a payment method:\n");
    printf("1. Visa\n");
    printf("2. MasterCard\n");
    printf("3. American Express\n");
}

struct seatinfo {
    char name[50];
    bool seat;
    int cost;
    int payment;


}

        seats[400][200];

void AFile(FILE *fp) {
    // Opens file or creates it (if necessary).
    fp = fopen("BirthdayMrG.txt", "wb");

    // For each seat the values are initialized.
    for (int d = 0; d < 400; d++) {
        for (int j = 0; j < 200; j++) {
            strcpy(seats[d][j].name, "");
            seats[d][j].payment = 0;
            seats[d][j].seat = false;

            // The prices depend on each section.

            if (j < 50 || j > 149) {

                if (d < 100) {
                    seats[d][j].cost = 50;
                } else if (d < 300) {
                    seats[d][j].cost = 35;
                } else {
                    seats[d][j].cost = 20;
                }

            } else {

                if (d < 5) {
                    seats[d][j].cost = 100;
                } else if (d < 10) {
                    seats[d][j].cost = 85;
                } else if (d < 50) {
                    seats[d][j].cost = 70;
                } else if (d < 100) {
                    seats[d][j].cost = 55;
                } else if (d < 250) {
                    seats[d][j].cost = 45;
                } else if (d < 350) {
                    seats[d][j].cost = 40;
                } else {
                    seats[d][j].cost = 30;
                }

            }
        }
    }

    fwrite(&seats, sizeof(seats), 1, fp);

}

void buy() {
    // Declaration of variables.
    char name[50];
    char option;
    int row;
    int first;
    int last;
    int seat;
    int payment;


    Zones();
    printf("Choose the zone where you want to sit:\n");
    printf("Or any other number to cancel.\n");
    scanf("%d", &option);

    switch (option) {
        case 1:
            first = 1;
            last = 5;
            break;
        case 2:
            first = 6;
            last = 10;
            break;
        case 3:
            first = 11;
            last = 50;
            break;
        case 4:
            first = 51;
            last = 100;
            break;
        case 5:
            first = 101;
            last = 250;
            break;
        case 6:
            first = 251;
            last = 350;
            break;
        case 7:
            first = 351;
            last = 400;
            break;
        case 8:
            first = 1;
            last = 100;
            break;
        case 9:
            first = 101;
            last = 300;
            break;
        case 10:
            first = 301;
            last = 400;
            break;
        default:
            printf("Back.\n");
            return;
    }

    do {
        printf("Choose a row between %d-%d", first, last);
        scanf("%d", &row);
    } while (row < first || row > last);

    if (option > 7) {
        do {
            printf("Choose a seat between 1-50 or 151-200");
            scanf("%d", &seat);
        } while ((seat < 1 || seat > 50) && (seat < 151 || seat > 200));

    } else {
        do {
            printf("Choose a seat between 51-150");
            scanf("%d", &seat);
        } while (seat < 51 || seat > 150);
    }

    PaymentMethod();
    printf("Select one payment method, or cancel with other number.\n");
    scanf("%d", &payment);

    if (payment < 1 || payment > 3) {
        printf("Back.\n");
        return;
    }

    printf("hi. What's your name?:");
    fflush(stdin);
    fgets(name, sizeof(name), stdin);

    printf("Enter O to accept, anything else to cancel.\n");
    scanf("%c", &option);

    if (!option) {

        if (seats[row - 1][seat - 1].seat) {
            printf("This seat is taken.\n");
        } else {
            seats[row - 1][seat - 1].seat = true;
            seats[row - 1][seat - 1].payment = payment;
            strcpy(seats[row - 1][seat - 1].name, name);
            printf("Transaction confirmed.\n");
        }

    } else{
        printf("Back.");
    }
}

int income(int first, int last, int firstseat, int lastseat, int sold) {
    int count = 0;
    int sales = 0;
    for (int d = first - 1; d < last; d++) {
        for (int j = firstseat - 1; j < lastseat; j++) {
            if (seats[d][j].seat) {
                count++;
                sales += seats[d][j].cost;
            }
        }
    }
    if (sold) {
        return count;
    }
    return sales; // Or it returns the total income.
}

// Function to sum the income of all zones.
int ZoneSold(int zone, int sold) {
    int count = 0;
    int first;
    int last;

    switch (zone) {
        case 1:
            first = 1;
            last = 5;
            break;
        case 2:
            first = 6;
            last = 10;
            break;
        case 3:
            first = 11;
            last = 50;
            break;
        case 4:
            first = 51;
            last = 100;
            break;
        case 5:
            first = 101;
            last = 250;
            break;
        case 6:
            first = 251;
            last = 350;
            break;
        case 7:
            first = 351;
            last = 400;
            break;
        case 8:
            first = 1;
            last = 100;
            break;
        case 9:
            first = 101;
            last = 300;
            break;
        case 10:
            first = 301;
            last = 400;
            break;
        default:
            first = 1;
            last = 200;
            break;
    }

    if (zone > 7) {
        count += income(first, last, 1, 50, sold);
        count += income(first, last, 151, 200, sold);
    } else {
        count += income(first, last, 51, 150, sold);
    }

    return count;
}

void Reports() {
    int option;
    int zone = 0;
    int count = 0;
    float rowsize;

    // Reports menu.
    Reports();
    printf("Choose an option, or any other number to return:\n");
    scanf("%d", &option);

    switch (option) {
        case 1:
            count = ZoneSold(zone, 1);
            printf("Total tickets sold: %d", count);
            break;
        case 2:
            do {
                zone();
                printf("Enter a zone:");
                scanf("%d", &zone);
            } while (zone < 1 || zone > 10);

            count = ZoneSold(zone, 1);
            printf("Total tickets sold in this zone: %d", count);
            break;
        case 3:
            count = ZoneSold(zone, 0);
            printf("Total income: $%d", count);
            break;
        case 4:
            do {
                zone();
                printf("Enter a zone:\n");
                scanf("%d", &zone);
            } while (zone < 1 || zone > 10);

            count = ZoneSold(zone, 0);
            printf("Total income in this zone: $%d", count);
            break;
        case 5:
            count = ZoneSold(zone, 1);
            printf("Occupation rate: %f%%", count * 100.0 / 80000);
            break;
        case 6:
            do {
                zone();
                printf("Enter a zone:");
                scanf("%d", &zone);
            } while (zone < 1 || zone > 10);
            count = ZoneSold(zone, 1);

            // The rows have different sizes depending on the zone.
            switch (zone) {
                case 1:
                case 2:
                    rowsize = 5;
                    break;
                case 3:
                    rowsize = 40;
                    break;
                case 4:
                case 6:
                case 7:
                    rowsize = 50;
                    break;
                case 8:
                case 10:
                    rowsize = 100;
                    break;
                case 5:
                    rowsize = 150;
                    break;
                case 9:
                default:
                    rowsize = 200;
                    break;
            }
            printf("Occupation rate in this zone: %f%%", count / rowsize);
            break;
        default:
            printf("Back");
            return;
    }

}

// This function modifies the file with the entered data.
void wFile(FILE *fp) {
    fp = fopen("MrG.txt", "wb");
    fwrite(&seats, sizeof(seats), 1, fp);
    fclose(fp);
}

int main() {

    // File pointer
    FILE *fp;
    int option;

    //Opens file.
    fp = fopen("mrg.txt", "rb");


    if (fp == NULL) {
        AFile(fp);
    } else {

        while (fread(&seats, sizeof(seats), 1, fp));
    }

    fclose(fp);


    do {

        MainMenu();
        scanf("%d", &option);
        fflush(stdin);

        switch (option) {
            case 1:
                buy();
                break;
            case 2:
                wFile(fp);
                printf("Data saved.\n");
                break;
            case 3:
                Reports();
                break;
            case 0:
                wFile(fp);
                printf("\nBye.\n");
                break;
            default:
                printf("\nNot valid.\n");
                break;
        }

    } while (option != '0');

    return 0;
}
