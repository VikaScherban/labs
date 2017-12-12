#Laba2
1.	�� ��������� download.file() ���������� ����� excel ���� � ������� http://data.gov.ua �� �������� ���� (xls, xlsx � ����� �������, ���� ���������� mode = �wb�. ������� ����� 6 ����� ���������� ������ �����.

```r
>install.packages("XML")
> library(XML)
> download.file("http://data.gov.ua/file/150098/download?token=J9U7YRrj", destfile="myfile.xml", mode = �wb�)
>xmldataframe <- xmlToDataFrame("myfile.xml")
> head(xmldataframe,6)
  element
1        
2    <NA>
3    <NA>
4    <NA>
5    <NA>
6    <NA>
                                                                                             AORG
1                                                                                            <NA>
2 Державне підприємство "Міжнародний аеропорт "Львів"
3 Державне підприємство "Міжнародний аеропорт "Львів"
4 Державне підприємство "Міжнародний аеропорт "Львів"
5 Державне підприємство "Міжнародний аеропорт "Львів"
6 Державне підприємство "Міжнародний аеропорт "Львів"
                  AYEAR           AQUARTER
1                  <NA>               <NA>
2 2015.0000000000000000 1.0000000000000000
3 2015.0000000000000000 1.0000000000000000
4 2015.0000000000000000 1.0000000000000000
5 2015.0000000000000000 1.0000000000000000
6 2015.0000000000000000 1.0000000000000000
             VPLACCOUNT                VAGENTCODE
1                  <NA>                      <NA>
2 2000.0000000000000000 24596990.0000000000000000
3 2000.0000000000000000 25264192.0000000000000000
4 2000.0000000000000000 33358979.0000000000000000
5 2000.0000000000000000                         0
6 2000.0000000000000000                         0
                                                                                          VAGENTNAME
1                                                                                               <NA>
2                                                                    КЮНЕ\n  I НАГЕЛЬ ДП
3 Універсальне\n  агенство з продажу авіаперевезень ПАТ
4                                                                           ТОВ\n  "БАКІТО"
5                                                                                         AVS\n  LTD
6                                                                               Challenge\n  Aero AG
  VCURRENCY           VQUANTITY             VREVCURRENCY
1      <NA>                <NA>                     <NA>
2       UAH  6.0000000000000000                        0
3       UAH  3.0000000000000000                        0
4       UAH  1.0000000000000000                        0
5       USD 51.0000000000000000 1897041.0000000000000000
6       USD  8.0000000000000000  103355.0000000000000000
                 VREVUAH
1                   <NA>
2  2679.0000000000000000
3    63.0000000000000000
4    37.0000000000000000
5 50657.0000000000000000
6  2723.0000000000000000
                                         VREVENUEDESCRIPT
1                                                    <NA>
2 послуги\n  комерційного складу
3                  послуги\n  паркування
4                          сервісні\n  збори
5  аеропортове\n  обслуговування
6  аеропортове\n  обслуговування
                                                                                                       VREVENUETYPE
1                                                                                                              <NA>
2 Чистий дохід від реалізації продукції (товарів, робіт, послуг)
3 Чистий дохід від реалізації продукції (товарів, робіт, послуг)
4 Чистий дохід від реалізації продукції (товарів, робіт, послуг)
5 Чистий дохід від реалізації продукції (товарів, робіт, послуг)
6 Чистий дохід від реалізації продукції (товарів, робіт, послуг)
          VUNITS
1           <NA>
2 послуга
3 послуга
4 послуга
5 послуга
6 послуга
```

2.	�� ��������� download.file() ���������� ���� getdata_data_ss06hid.csv �� ���������� https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv �� ���������� ��� � R. Code book, �� ������� �������� ������ ����������� �� ���������� https://www.dropbox.com/s/dijv0rlwo4mryv5/PUMSDataDict06.pdf?dl=0  ��������� ������, ������ property ����� value $1000000+

```r
> download.file("https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv", destfile="csvfile.csv")
> X<-read.csv(file="csvfile.csv", header=TRUE)
> sum(X$VAL > 1000000, na.rm = TRUE)
[1] 0
```

3.	�������� xml ���� �� ���������� http://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Frestaurants.xml ������ ��������� ����� zipcode 21231?

```r
> library(XML)
> download.file("http://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Frestaurants.xml", destfile="file.xml")
>doc = xmlParseDoc("file.xml")
>listxml <- xpathSApply(doc,"//zipcode",xmlValue)
> sum(listxml== 21231)
[1] 127
```
