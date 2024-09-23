ЗАДАЧА 1. Вывести служебную информацию о пакете matplotlib (Python). Разобрать основные элементы содержимого файла со служебной информацией из пакета. Как получить пакет без менеджера пакетов, прямо из репозитория?
  РЕШЕНИЕ: 
  ```bash
  pip show matplotlib
  ```

  ![Снимок экрана от 2024-09-16 12-49-38](https://github.com/user-attachments/assets/80502082-8ed9-46ba-ae71-5134f08d2fdf)
  
  Name: Имя пакета (например, matplotlib).
  Version: Текущая версия пакета.
  Summary: Краткое описание пакета.
  Home-page: Ссылка на домашнюю страницу пакета.
  Author/Author-email: Имя и email автора.
  License: Лицензия, по которой распространяется пакет.

  Получение пакета прямо из репозитория:

  ```bash
  git clone https://github.com/matplotlib/matplotlib.git
  cd matplotlib
  pip install .
  ```

  ![image](https://github.com/user-attachments/assets/06379a90-addf-43ea-a49a-e6cc0b266a1f)
  ![image](https://github.com/user-attachments/assets/bde781d8-0ab6-4ae6-87c6-582668485223)


ЗАДАЧА 2. Вывести служебную информацию о пакете express (JavaScript). Разобрать основные элементы содержимого файла со служебной информацией из пакета. Как получить пакет без менеджера пакетов, прямо из репозитория?
  РЕШЕНИЕ: 
  ```bash
  npm show express
  ```

  ![image](https://github.com/user-attachments/assets/61053961-076d-40dd-bb6c-8da8fa74de16)

  name: Имя пакета.
  version: Текущая версия пакета.
  description: Краткое описание пакета.
  main: Главный файл, с которого начинается выполнение пакета.
  scripts: Список пользовательских команд, которые можно выполнять с помощью команды npm run. Например, это может быть команда для запуска тестов или сборки проекта.
  dependencies: Зависимости, которые необходимы для работы пакета. Это перечень других библиотек с указанием их версий.
  devDependencies: Зависимости для разработки (необязательные для работы пакета в продакшн среде).
  license: Лицензия, под которой распространяется пакет.
  repository: URL репозитория, в котором хранится код проекта.
  author: Имя и контактная информация автора.
  keywords: Список ключевых слов, связанных с проектом, которые могут помочь найти его в каталоге NPM.

  Получение пакета прямо из репозитория:

  ```bash
  git clone https://github.com/expressjs/express.git
  cd express
  npm install
  ```

  ![image](https://github.com/user-attachments/assets/61249034-d570-4297-a83c-c0c6793fd9c3)


ЗАДАЧА 3. Сформировать graphviz-код и получить изображения зависимостей matplotlib и express.
  РЕШЕНИЕ: 
  
  ```bash
  dot -Tpng express_dependencies.dot -o express_dependencies.png
  dot -Tpng matplotlib_dependencies.dot -o matplotlib_dependencies.png
```

  ![image](https://github.com/user-attachments/assets/ea544ab2-652f-410e-93d3-134acf82f304)
  ![image](https://github.com/user-attachments/assets/4143d6b5-76fb-4683-877f-6c8f738dfe2f)
  ![express_dependencies](https://github.com/user-attachments/assets/01837661-91c1-4ace-af58-6602f6140ae9)
  ![matplotlib_dependencies](https://github.com/user-attachments/assets/a8c99236-818a-4be8-9c90-772eb0007a50)


ЗАДАЧА 4. Изучить основы программирования в ограничениях. Установить MiniZinc, разобраться с основами его синтаксиса и работы в IDE.
Решить на MiniZinc задачу о счастливых билетах. Добавить ограничение на то, что все цифры билета должны быть различными (подсказка: используйте all_different). Найти минимальное решение для суммы 3 цифр.
  РЕШЕНИЕ: 
  
```minizinc
  include "alldifferent.mzn";  % Подключаем библиотеку для alldifferent

  % Определяем массив для хранения 6 цифр билета
  array[1..6] of var 0..9: digits;
  
  % Ограничение: все цифры должны быть различными
  constraint alldifferent(digits);
  
  % Ограничение: сумма первых трёх цифр должна равняться сумме последних трёх
  constraint sum(digits[1..3]) = sum(digits[4..6]);
  
  % Целевая функция: минимизируем сумму первых трёх цифр
  solve minimize sum(digits[1..3]);
  
  % Выводим результат
  output [
      "Digits: ", show(digits), 
      "\nSum of first 3 digits: ", show(sum(digits[1..3])), 
      "\nSum of last 3 digits: ", show(sum(digits[4..6]))
  ];
```

  ![Снимок экрана 2024-09-22 214850](https://github.com/user-attachments/assets/5b4ab1ef-1238-47aa-8c17-3f6a9ae03118)
  ![Снимок экрана 2024-09-22 214931](https://github.com/user-attachments/assets/9923e75c-83c8-4736-bb04-6b51e5803d12)


ЗАДАЧА 5. Решить на MiniZinc задачу о зависимостях пакетов для рисунка, приведенного ниже. https://github.com/true-grue/kisscm/blob/main/pract/images/pubgrub.png

  РЕШЕНИЕ: 
  
```minizinc
  % Определяем пакеты
  enum PACKAGES = {
      root, 
      menu_1_0_0, menu_1_1_0, menu_1_2_0, menu_1_3_0, menu_1_4_0, menu_1_5_0, 
      dropdown_2_0_0, dropdown_2_1_0, dropdown_2_2_0, dropdown_2_3_0, dropdown_1_8_0,
      icons_1_0_0, icons_2_0_0
  };
  
  % Переменные, указывающие, установлен ли пакет (1) или нет (0)
  array[PACKAGES] of var 0..1: installed;
  
  % Обязательно устанавливаем root
  constraint
      installed[root] == 1;
  
  % Ограничения зависимостей
  constraint
      (installed[root] == 1) -> (installed[menu_1_0_0] == 1 /\ installed[menu_1_5_0] == 1 /\ installed[icons_1_0_0] == 1) /\
      (installed[menu_1_5_0] == 1) -> (installed[dropdown_2_3_0] == 1 /\ installed[dropdown_2_0_0] == 1) /\
      (installed[menu_1_4_0] == 1) -> (installed[dropdown_2_3_0] == 1 /\ installed[dropdown_2_0_0] == 1) /\
      (installed[menu_1_3_0] == 1) -> (installed[dropdown_2_3_0] == 1 /\ installed[dropdown_2_0_0] == 1) /\
      (installed[menu_1_2_0] == 1) -> (installed[dropdown_2_3_0] == 1 /\ installed[dropdown_2_0_0] == 1) /\
      (installed[menu_1_1_0] == 1) -> (installed[dropdown_2_3_0] == 1 /\ installed[dropdown_2_0_0] == 1) /\
      (installed[menu_1_0_0] == 1) -> (installed[dropdown_1_8_0] == 1) /\
      (installed[dropdown_2_0_0] == 1) -> (installed[icons_2_0_0] == 1) /\
      (installed[dropdown_2_1_0] == 1) -> (installed[icons_2_0_0] == 1) /\
      (installed[dropdown_2_2_0] == 1) -> (installed[icons_2_0_0] == 1) /\
      (installed[dropdown_2_3_0] == 1) -> (installed[icons_2_0_0] == 1);
  
  % Целевая функция: минимизируем количество установленных пакетов
  solve minimize sum(installed);
  
  % Выводим результат
  output [
      "Installed packages: ", show(installed)
  ];
```

  ![Снимок экрана 2024-09-22 221309](https://github.com/user-attachments/assets/9aedc894-8d3e-4e55-a5dd-9e2b513afd13)


ЗАДАЧА 6. Решить на MiniZinc задачу о зависимостях пакетов для следующих данных:
          root 1.0.0 зависит от foo ^1.0.0 и target ^2.0.0.
          foo 1.1.0 зависит от left ^1.0.0 и right ^1.0.0.
          foo 1.0.0 не имеет зависимостей.
          left 1.0.0 зависит от shared >=1.0.0.
          right 1.0.0 зависит от shared <2.0.0.
          shared 2.0.0 не имеет зависимостей.
          shared 1.0.0 зависит от target ^1.0.0.
          target 2.0.0 и 1.0.0 не имеют зависимостей.

  РЕШЕНИЕ: 
  
```minizinc
  % Определяем пакеты
  enum PACKAGES = {
      root, 
      foo_1_0_0, foo_1_1_0, 
      left_1_0_0, right_1_0_0, 
      shared_1_0_0, shared_2_0_0, 
      target_1_0_0, target_2_0_0
  };
  
  % Переменные, указывающие, установлен ли пакет (1) или нет (0)
  array[PACKAGES] of var 0..1: installed;
  
  % Ограничения зависимостей
  constraint
      (installed[root] == 1) -> (installed[foo_1_1_0] == 1 /\ installed[target_2_0_0] == 1) /\
      (installed[foo_1_1_0] == 1) -> (installed[left_1_0_0] == 1 /\ installed[right_1_0_0] == 1) /\
      (installed[left_1_0_0] == 1) -> (installed[shared_1_0_0] == 1) /\
      (installed[right_1_0_0] == 1) -> (installed[shared_2_0_0] == 1) /\ (installed[shared_1_0_0] == 0) /\
      (installed[shared_1_0_0] == 1) -> (installed[target_1_0_0] == 1);
  
  % Обязательно устанавливаем root
  constraint
      installed[root] == 1;
  
  % Целевая функция: минимизируем количество установленных пакетов
  solve minimize sum(installed);
  
  % Выводим результат
  output [
      "Installed packages: ", show(installed)
  ];
```

  ![Снимок экрана 2024-09-22 221858](https://github.com/user-attachments/assets/e22cd150-dd76-454d-bef1-0dd03da6193f)
  ![Снимок экрана 2024-09-22 221920](https://github.com/user-attachments/assets/5f198866-265a-40ee-a211-7b5dff42324c)


ЗАДАЧА 7. Представить задачу о зависимостях пакетов в общей форме. Здесь необходимо действовать аналогично реальному менеджеру пакетов. То есть получить описание пакета, а также его зависимости в виде структуры данных. Например, в виде словаря. В предыдущих задачах зависимости были явно заданы в системе ограничений. Теперь же систему ограничений надо построить автоматически, по метаданным.

  РЕШЕНИЕ:

  ```python
  # Пример структуры данных с зависимостями и версиями
  packages = {
      "root": {"dependencies": ["foo", "target"], "version": None},
      "foo": {"dependencies": ["left", "right"], "version": None},
      "left": {"dependencies": ["shared>=1.0.0"], "version": None},
      "right": {"dependencies": ["shared<2.0.0"], "version": None},
      "shared": {"dependencies": [], "version": None},
      "target": {"dependencies": [], "version": None},
  }
  
  def generate_minizinc_code(packages):
      package_names = ', '.join(packages.keys())
      # Генерация массива установленных пакетов
      minizinc_code = f"enum PACKAGES = {{{package_names}}};\n"
      minizinc_code += "array[PACKAGES] of var 0..1: installed;\n\n"
      # Добавляем условие для root
      minizinc_code += "constraint installed[root] == 1;\n"
      # Генерация ограничений
      for package, details in packages.items():
          dependencies = details["dependencies"]
          if dependencies:
              dep_constraints = []
              for dep in dependencies:
                  if '>' in dep or '<' in dep or '=' in dep:
                      dep_name = dep.split('>=')[0].split('<')[0].split('=')[0]
                      dep_constraints.append(f"installed[{dep_name}] == 1")
                  else:
                      dep_constraints.append(f"installed[{dep}] == 1")
              constraint = "constraint installed[{}] == 1 -> ({});\n".format(
                  package, ' /\\ '.join(dep_constraints)
              )
              minizinc_code += constraint
      minizinc_code += "\nsolve minimize sum(installed);\n"
      minizinc_code += 'output ["Installed packages: ", show(installed)];\n'
      return minizinc_code
  
  
  # Генерация и вывод MiniZinc кода
  minizinc_code = generate_minizinc_code(packages)
  print(minizinc_code)
```

  ВЫВОД:
  
  ```minizinc
  enum PACKAGES = {root, foo, left, right, shared, target};
  array[PACKAGES] of var 0..1: installed;
  
  constraint installed[root] == 1;
  constraint installed[root] == 1 -> (installed[foo] == 1 /\ installed[target] == 1);
  constraint installed[foo] == 1 -> (installed[left] == 1 /\ installed[right] == 1);
  constraint installed[left] == 1 -> (installed[shared] == 1);
  constraint installed[right] == 1 -> (installed[shared] == 1);
  
  solve minimize sum(installed);
  output ["Installed packages: ", show(installed)];
```

  ВЫВОД MiniZinc:
  Installed packages: [1, 1, 1, 1, 1, 1]
