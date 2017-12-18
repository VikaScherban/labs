#Laba5
В цій лабораторній роботі необхідно зчитати WEB сторінку з сайту IMDB.com зі 100 фільмами 2017 року виходу за посиланням «http://www.imdb.com/search/title?count=100&release_date=2017,2017&title_type=feature».  Необхідно створити data.frame «movies» з наступними даними: номер фільму (rank_data), назва фільму (title_data), тривалість (runtime_data). Для виконання лабораторної рекомендується використати бібліотеку «rvest». CSS селектори для зчитування необхідних даних: rank_data: «.text-primary», title_data: «.lister-item-header a», runtime_data: «.text-muted .runtime». Для зчитування url використовується функція read_html, для зчитування даних по CSS селектору – html_nodes і для перетворення зчитаних html даних в текст - html_text. Рекомендується перетворити rank_data та runtime_data з тексту в числові значення. При формуванні дата фрейму функцією data.frame рекомендується використати параметр «stringsAsFactors = FALSE».
В результаті виконання лабораторної роботи необхідно відповісти на запитання:


>install.packages("rvest")
>library(rvest)
>lego_movie <- read_html("http://www.imdb.com/search/title?count=100&release_date=2017,2017&title_type=feature")
>rank_data_html<-html_nodes(lego_movie,'.text-primary')
>rank_data <- html_text(rank_data_html)
>rank_data<-as.numeric(rank_data)

>title_data_html <- html_nodes(lego_movie,'.lister-item-header a')
>title_data <- html_text(title_data_html)

>runtime_data_html <- html_nodes(lego_movie,'.text-muted .runtime')
>runtime_data <- html_text(runtime_data_html)

#Видаляємо підстроку min d runtime_data
>runtime_data<-gsub(" min","",runtime_data)
#Приводимо до numeric runtime_data
>runtime_data<-as.numeric(runtime_data)

#DF movies
>movies <- data.frame(Rank = rank_data, Title = title_data, Runtime = runtime_data, stringsAsFactors = FALSE )

1.Виведіть перші 6 назв фільмів дата фрейму.
>head(movies$Title, 6)

[1] "Зорянi вiйни: Останнi Джедаi"   "The Disaster Artist"           
[3] "The Shape of Water"             "Лiга справедливостi"           
[5] "Jumanji: Welcome to the Jungle" "Тор: Рагнарок"   

2.Виведіть всі назви фільмів с тривалістю більше 120 хв.
>movies[movies$Runtime > 120, ]$Title
[1] "Зорянi вiйни: Останнi Джедаi"             "The Shape of Water"                      
 [3] "Тор: Рагнарок"                            "Mother!"                                 
 [5] "Kingsman: Золоте кiльце"                  "Вартовi Галактики 2"                     
 [7] "Воно"                                     "The Killing of a Sacred Deer"            
 [9] "Darkest Hour"                             "Call Me by Your Name"                    
[11] "Той, хто бiжить по лезу 2049"             "Валерiан i мiсто тисячi планет"          
[13] "Логан: Росомаха"                          "Phantom Thread"                          
[15] "Downsizing"                               "Диво-Жiнка"                              
[17] "Людина-павук: Повернення додому"          "Detroit"                                 
[19] "All the Money in the World"               "Molly's Game"                            
[21] "Сiм сестер"                               "Красуня i Чудовисько"                    
[23] "Вiйна за планету мавп"                    "Mudbound"                                
[25] "The Square"                               "Roman J. Israel, Esq."                   
[27] "Пiрати Карибського моря: Помста Салазара" "Трансформери: Останнiй лицар"            
[29] "Пострiл в безодню"                        "Power Rangers"                           
[31] "Hostiles"                                 "Girls Trip"                              
[33] "Джон Уiк 2"                              

3.Скільки фільмів мають тривалість менше 100 хв.
>length(movies[movies$Runtime < 100, ]$Title)
[1] 20