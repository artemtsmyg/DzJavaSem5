//1) Подсчитать количество вхождения каждого слова
//        Пример:
//        Россия идет вперед всей планеты. Планета — это не Россия.
//        toLoverCase().
//        (Усложнение - игнорировать пунктуацию)*

import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;

class Lesson5z1 {
    public static void main(String[] args) {
        Ex1();
        //Ex2();
        //Ex3();
    }
    public static void Ex3() {

        String[] array1 = {"qwe", "asd", "qwe", "x"};
        String[] array2 = {"qwe", "v"};

        Map<String, Integer> mapArray1 = getCountWords(array1);
        Map<String, Integer> mapArray2 = getCountWords(array2);

        Map<String, Integer> mapResult = new HashMap<>();
        for (Map.Entry<String, Integer> entry : mapArray1.entrySet()) {
            String key = entry.getKey();
            int countMap1 = entry.getValue();
            int countMap2 = mapArray2.getOrDefault(key, 0);
            if (countMap2 > 0) {
                mapResult.put(key, countMap1 + countMap2);
            }
        }

        for (Map.Entry<String, Integer> entry : mapResult.entrySet()) {
            System.out.println(entry.getKey() + "=" + entry.getValue());
        }

    }

    public static void Ex2() {

        String text = "Россия идет вперед всей планеты. Планета — это не Россия.";
        text = text.replaceAll("[-|–|—]|\\p{Punct}", " ");
        while (text.contains("  ")) {
            text = text.replace("  ", " ");
        }

        String findWord = "Россия";

        String[] arrayText = text.split(" ");
        Map<String, Integer> map = new HashMap<>();
        for (String currentWord : arrayText) {
            if (!findWord.toLowerCase().equals(currentWord.toLowerCase())) {
                continue;
            }

            int count = map.getOrDefault(findWord.toLowerCase(), 0);
            map.put(currentWord.toLowerCase(), ++count);
        }

        System.out.println("Количество искомого слова: " + map.getOrDefault(findWord.toLowerCase(), 0));

    }

    public static void Ex1() {
        String text = "Россия идет вперед всей планеты. Планета — это не Россия.";
        text = text.replaceAll("[-|–|—]|\\p{Punct}", " ");
        while (text.contains("  ")) {
            text = text.replace("  ", " ");
        }
        String[] arrayText = text.split(" ");

        Map<String, Integer> map = getCountWords(arrayText);

        for (Map.Entry<String, Integer> entry : map.entrySet()) {
            System.out.println(entry.getKey() + " - " + entry.getValue());
        }
    }

    public static Map<String, Integer> getCountWords(String[] array) {
        Map<String, Integer> map = new HashMap<>();

        for (String current : array) {
            int count = map.getOrDefault(current.toLowerCase(), 0);
            map.put(current.toLowerCase(), ++count);
        }

        return map;

    }
}







//2) Пусть дан список сотрудников:
//
//        Иван Иванов
//
//        Светлана Петрова
//
//        Кристина Белова
//
//        Анна Мусина
//
//        Анна Крутова
//
//        Иван Юрин
//
//        Петр Лыков
//
//        Павел Чернов
//
//        Петр Чернышов
//
//        Мария Федорова
//
//        Марина Светлова
//
//        Мария Савина
//
//        Мария Рыкова
//
//        Марина Лугова
//
//        Анна Владимирова
//
//        Иван Мечников
//
//        Петр Петин
//
//        Иван Ежов
//
//        Написать программу, которая найдёт и выведет повторяющиеся имена с количеством повторений.
//        Отсортировать по убыванию популярности.

import java.util.Comparator;
import java.util.HashMap;
import java.util.LinkedHashMap;
import java.util.Map;
import java.util.stream.Collectors;


class Lesson5z2 {
   public static void main(String[] args) {
       Map<String, Integer> namePeople = new HashMap<>();
       String[] staff = {
               "Иван Иванов",
               "Светлана Петрова",
               "Кристина Белова",
               "Анна Мусина",
               "Анна Крутова",
               "Иван Юрин",
               "Петр Лыков",
               "Павел Чернов",
               "Петр Чернышов",
               "Мария Федорова",
               "Марина Светлова",
               "Мария Савина",
               "Мария Рыкова",
               "Марина Лугова",
               "Анна Владимирова",
               "Иван Мечников",
               "Петр Петин",
               "Иван Ежов"
       };
       countName(staff, namePeople);
       sortedStaff(namePeople);

   }
   public static void countName(String[] people, Map<String, Integer> namePeople) {
       for (String person : people) {
           String name = person.split(" ")[0];
           if (namePeople.containsKey(name)) {
               namePeople.put(name, namePeople.get(name) + 1);
           } else {
               namePeople.put(name, 1);
           }
       }
   }
   public static void sortedStaff(Map<String, Integer> namePeople) {
       Map<String, Integer> sortedName = namePeople.entrySet().stream()
               .sorted(Comparator.comparingInt(e -> -e.getValue()))
               .collect(Collectors.toMap(
                       Map.Entry::getKey,
                       Map.Entry::getValue,
                       (a, b) -> {
                           throw new AssertionError();
                       },
                       LinkedHashMap::new));

       sortedName.entrySet().forEach(System.out::println);
   }
}
