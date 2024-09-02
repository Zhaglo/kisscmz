ЗАДАЧА 1. Вывести отсортированный в алфавитном порядке список имен пользователей в файле passwd.
  РЕШЕНИЕ:
  cut -d: -f1 /etc/passwd | sort
  ![image](https://github.com/user-attachments/assets/3142e02b-3e12-4937-bca1-e1bd04e341aa)

ЗАДАЧА 2. Вывести данные /etc/protocols в отформатированном и отсортированном порядке для 5 наибольших портов.
  РЕШЕНИЕ:
  cat /etc/protocols |sort -nrk2 | head -n 5 | awk '{print $2, $1}'
  ![image](https://github.com/user-attachments/assets/5c4fa12e-fe3a-44af-b922-80ca49da2be9)

ЗАДАЧА 3. Написать программу banner средствами bash для вывода текстов.
  РЕШЕНИЕ:
  string='MIREA'
  size=${#string}
  echo -n "+"
  for ((i=-2;i<size;i++))
  do
  echo -n "-"
  done
  echo "+"
  echo "| $string |"
  echo -n "+"
  for ((i=-2;i<size;i++))
  do
  echo -n "-"
  done
  echo "+"
  +-------+
  | MIREA |
  +-------+
  ![Снимок экрана от 2024-09-02 17-43-27](https://github.com/user-attachments/assets/3dee2459-5baf-4ee4-8e10-70b5c5a37d62)
