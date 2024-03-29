<template>
  <div class="main bg-gray-900 text-white font-sans">
    <div class="flex items-center justify-center h-screen p-4">
      <div
        class="max-w-lg mx-auto bg-gray-800 rounded shadow-lg overflow-hidden"
      >
        <transition mode="out-in">
          <div class="p-4" :key="activeQuestionIdx">
            <h1 class="text-xl font-semibold mb-2">
              {{ activeQuestionIdx + 1 }}. {{ question.question }}
            </h1>
            <p class="text-gray-400">
              {{ question.answer }}
            </p>
          </div>
        </transition>
        <div class="p-4 bg-gray-700 flex justify-between gap-4">
          <button
            class="bg-gray-800 text-white py-1 px-4 w-1/3 rounded uppercase"
            @click="prevQuestion"
          >
            Prev
          </button>
          <button
            class="bg-gray-800 text-white py-1 px-4 w-1/3 rounded uppercase"
            @click="isOpen = true"
          >
            Select
          </button>
          <button
            class="bg-gray-800 text-white py-1 px-4 w-1/3 rounded uppercase"
            @click="nextQuestion"
          >
            Next
          </button>
        </div>
      </div>
    </div>

    <div
      id="overlay"
      class="fixed top-0 left-0 w-full h-full bg-black opacity-25 z-50"
      :class="isOpen ? '' : 'hide'"
      @click="isOpen = false"
    ></div>

    <div
      id="modal"
      class="fixed top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 p-4 z-50 h-3/6 w-full max-w-lg"
      :class="isOpen ? '' : 'hide'"
    >
      <div
        class="rounded-md shadow-lg p-4 bg-gray-800 h-full overflow-y-hidden"
      >
        <ul class="overflow-y-auto h-full">
          <li
            class="mb-2 cursor-pointer hover:bg-gray-700 p-2 rounded"
            :class="activeQuestionIdx === idx ? 'bg-gray-700' : ''"
            v-for="(question, idx) in questions"
            :key="question"
            @click="
              activeQuestionIdx = idx;
              isOpen = false;
            "
          >
            {{ idx + 1 }}. {{ question.question }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from "vue";
const isOpen = ref(false);

const questions = ref([
  {
    question:
      "Предпосылки появления баз данных. История развития технологий хранения и обработки данных.",
    answer:
      "Предпосылки включают рост объемов данных, необходимость эффективного их хранения и поиска. Развитие технологий началось с использования файловой системы, затем появилась иерархическая и сетевая модели данных, а затем реляционная модель, которая привела к появлению баз данных.",
  },
  {
    question:
      "База данных и информационная система. Понятие информации и данных.",
    answer:
      "База данных - это организованная коллекция данных, предназначенная для эффективного поиска, хранения и обработки. Информационная система включает в себя базу данных, программное обеспечение и пользователей. Данные - это факты, а информация - это данные, организованные и интерпретированные таким образом, чтобы быть полезными.",
  },
  {
    question:
      "Объясните смысл следующих терминов и приведите их примеры: данные, информация, информационная система, предметная область, база данных, СУБД.",
    answer:
      "Данные: Набор необработанных фактов (например, числа, текст). Информация: Данные, обработанные и организованные для принятия решений. Информационная система: Совокупность оборудования, программ и людей, работающих вместе для обработки данных. Предметная область: Область знаний или деятельности, для которой создается информационная система. База данных: Структурированная коллекция данных, организованная для эффективного доступа и управления. СУБД (система управления базами данных): Программное обеспечение для создания, управления и обновления баз данных.",
  },
  {
    question: "База данных. Структурирование данных. Классификация.",
    answer:
      "База данных - организованная коллекция данных. Структурирование данных включает в себя определение типов данных и их взаимосвязей. Классификация баз данных может быть реляционной, иерархической, сетевой и др.",
  },
  {
    question:
      "Основные понятия и структура базы данных (БД). Основные элементы БД и их общая характеристика.",
    answer:
      "Основные элементы включают таблицы (в реляционной модели), записи, поля, ключи и связи. База данных организована так, чтобы обеспечивать эффективное хранение, поиск и обработку данных.",
  },
  {
    question: "Классификация и функции СУБД.",
    answer:
      "Классификация включает реляционные, объектно-ориентированные, иерархические и др. Функции СУБД включают создание, обновление, запросы и управление базой данных.",
  },
  {
    question: "Обзор современных СУБД, их характеристики и возможности.",
    answer:
      "Современные СУБД включают MySQL, Oracle, Microsoft SQL Server. Характеристики включают производительность, надежность и поддержку различных типов данных.",
  },
  {
    question: "Сетевые принципы доступа к данным. Технология «клиент-сервер».",
    answer:
      "Сетевые принципы включают в себя удаленный доступ и обмен данными между компьютерами. Технология 'клиент-сервер' разделяет функциональность между клиентом (пользовательским приложением) и сервером (обработка данных).",
  },
  {
    question: "Архитектура и типы СУБД.",
    answer:
      "Архитектура включает в себя одноранговую и клиент-серверную. Типы СУБД включают реляционные, объектно-ориентированные, временные и др.",
  },
  {
    question:
      "Трехуровневая сетевая архитектура баз данных. Понятие «тонкий» и «толстый» клиент.",
    answer:
      "Трехуровневая архитектура включает уровень данных, бизнес-логики и пользовательский интерфейс. 'Тонкий' клиент требует минимальной обработки на стороне клиента, в то время как 'толстый' клиент выполняет большую часть обработки на стороне клиента.",
  },
  {
    question:
      "Модель файлового сервера (модель удаленного управления данными). Достоинства и недостатки.",
    answer:
      "Модель файлового сервера включает центральное управление данными. Достоинства: простота, легкость в реализации. Недостатки: ограниченная масштабируемость, сложность обеспечения целостности данных.",
  },
  {
    question:
      "Принципы построения базы данных (БД). Архитектура организации БД.",
    answer:
      "Принципы включают минимизацию избыточности, обеспечение целостности данных, управление доступом. Архитектура БД включает в себя трехуровневую структуру: уровень данных, бизнес-логики и пользовательский интерфейс.",
  },
  {
    question:
      "Понятие моделей данных. Общая классификация моделей данных и их характеристика.",
    answer:
      "Модели данных - это абстракции, представляющие структуру данных и их взаимосвязи. Классификация включает иерархические, сетевые, реляционные и объектно-ориентированные модели с различными характеристиками.",
  },
  {
    question:
      "Основные модели представления данных. Иерархическая модель и ее общая характеристика. Достоинства, особенности и недостатки. Примеры.",
    answer:
      "Иерархическая модель представляет данные в виде древовидной структуры. Достоинства: простота. Недостатки: ограниченная гибкость. Пример: IMS (Information Management System).",
  },
  {
    question:
      "Основные модели представления данных. Сетевая модель и ее общая характеристика. Достоинства, особенности и недостатки. Примеры.",
    answer:
      "Сетевая модель представляет данные в виде сети. Достоинства: более гибкая структура. Недостатки: сложность. Пример: CODASYL.",
  },
  {
    question:
      "Основные модели представления данных. Реляционная модель и ее общая характеристика. Достоинства, особенности и недостатки. Примеры.",
    answer:
      "Реляционная модель представляет данные в виде таблиц. Достоинства: простота, гибкость. Недостатки: производительность при сложных запросах. Пример: MySQL, PostgreSQL.",
  },
  {
    question: "Этапы проектирования базы данных.",
    answer:
      "Этапы включают анализ требований, проектирование концептуальной модели, проектирование логической модели, проектирование физической модели и реализацию.",
  },
  {
    question:
      "Функциональные зависимости. Нормальные формы (1НФ, 2НФ, 3НФ, НФБК). Нормальные формы более высоких порядков.",
    answer:
      "Функциональные зависимости определяют взаимосвязи между атрибутами. Нормальные формы включают 1НФ (первая нормальная форма), 2НФ (вторая нормальная форма), 3НФ (третья нормальная форма) и др. Нормальные формы более высоких порядков включают 4НФ, 5НФ и т.д.",
  },
  {
    question:
      "Проектирование реляционных БД на основе принципов нормализации. Цель нормализации. Нормальные формы отношений.",
    answer:
      "Цель нормализации - минимизация избыточности данных и обеспечение их целостности. Нормальные формы отношений включают 1НФ, 2НФ, 3НФ и др., каждая из которых устраняет определенные виды избыточности.",
  },
  {
    question:
      "Технология нормализации реляционных таблиц. Достоинства и недостатки нормализации.",
    answer:
      "Технология включает разделение таблиц на более мелкие с целью устранения избыточности. Достоинства: обеспечение целостности данных. Недостатки: возможное усложнение запросов и производительность.",
  },
  {
    question:
      "Объясните смысл следующих основных понятий реляционной модели данных и приведите примеры: реляционная база данных, отношение, схема отношения, сущность, атрибут, домен, кортеж, первичный ключ.",
    answer:
      "Реляционная база данных: Совокупность связанных отношений. Отношение: Таблица с данными, представляющая сущность. Схема отношения: Определение структуры отношения. Сущность: Объект, который хранится в базе данных. Атрибут: Характеристика сущности. Домен: Множество возможных значений атрибута. Кортеж: Строка в отношении. Первичный ключ: Уникальный идентификатор кортежа.",
  },
  {
    question: "Понятие и основные свойства отношения.",
    answer:
      "Отношение представляет собой таблицу с данными, где каждая строка - кортеж, а каждый столбец - атрибут. Основные свойства: уникальность кортежей, уникальность столбцов, однозначность и неизменяемость данных.",
  },
  {
    question: "Реляционные модели. Понятие и свойства отношений.",
    answer:
      "Реляционные модели описывают структуру данных в виде отношений. Отношения обладают свойствами: уникальность кортежей, уникальность столбцов, однозначность и неизменяемость данных.",
  },
  {
    question:
      "Понятие ключа отношения. Необходимость задания ключей. Виды ключей. Свойства ключа. Примеры.",
    answer:
      "Ключ отношения - это атрибут или набор атрибутов, позволяющих однозначно идентифицировать кортеж в отношении. Ключи включают первичные, внешние и другие. Свойства ключа: уникальность и минимальность. Пример: первичный ключ 'ID' в таблице 'Сотрудники'.",
  },
  {
    question: "Виды связей между объектами и их отражение в модели.",
    answer:
      "Связи между объектами могут быть однозначными (один к одному, один ко многим) и многозначными (многие ко многим). Отражаются в модели с использованием внешних ключей.",
  },
  {
    question: "Ограничения целостности: понятие и классификация. Примеры.",
    answer:
      "Ограничения целостности обеспечивают правильность данных. Классификация: сущностные, ссылочные, доменные ограничения. Пример: NOT NULL - ограничение на отсутствие пустых значений.",
  },
  {
    question:
      "Понятие ссылочной целостности (целостности связи). Стратегии поддержания ссылочной целостности. Примеры.",
    answer:
      "Ссылочная целостность гарантирует существование связанных данных. Стратегии: CASCADE (каскадное обновление/удаление), SET NULL (установка в NULL), SET DEFAULT (установка в значение по умолчанию). Пример: CASCADE - при удалении родительской записи удаляются и связанные дочерние записи.",
  },
  {
    question:
      "Реляционная алгебра как формальная система манипулирования отношениями в реляционной модели данных. Свойство замкнутости. Краткий обзор операций реляционной алгебры.",
    answer:
      "Реляционная алгебра - это формальная система операций над отношениями. Свойство замкнутости гарантирует, что результаты операций также являются отношениями. Операции включают выборку, проекцию, соединение и т.д.",
  },
  {
    question: "Унарные операции реляционной алгебры: описание, примеры.",
    answer:
      "Унарные операции выполняются над одним отношением. Примеры: выборка (σ), проекция (π), переименование (ρ).",
  },
  {
    question: "Бинарные операции реляционной алгебры: описание, примеры.",
    answer:
      "Бинарные операции выполняются над двумя отношениями. Примеры: объединение (∪), пересечение (∩), декартово произведение (×).",
  },
  {
    question:
      "Жизненный цикл БД. Этапы ЖЦ БД. Уровни моделей и этапы проектирования БД. Разделение логического и физического представления данных.",
    answer:
      "Жизненный цикл БД включает этапы: определение требований, проектирование, реализация, эксплуатация и сопровождение. Уровни моделей: концептуальный, логический, физический. Этапы проектирования: концептуальное, логическое, физическое. Разделение логического (структура данных) и физического (хранилище данных) представления данных.",
  },
  {
    question:
      "Этапы проектирования: исследование проблемы, этап анализа, проектирование, реализация, внедрение, сопровождение.",
    answer:
      "Исследование проблемы - изучение потребностей. Анализ - выявление требований. Проектирование - создание структуры данных. Реализация - создание БД. Внедрение - внедрение в рабочую среду. Сопровождение - поддержка и модификации.",
  },
  {
    question: "Логическое проектирование баз данных.",
    answer:
      "Логическое проектирование включает определение структуры данных (таблицы, ключи) без привязки к конкретной СУБД. Создается логическая модель базы данных.",
  },
  {
    question: "Концептуальное проектирование баз данных. Объекты и атрибуты.",
    answer:
      "Концептуальное проектирование определяет сущности и их атрибуты независимо от конкретных технических решений. Объекты - сущности, атрибуты - характеристики сущностей.",
  },
  {
    question: "Концептуальные модели данных. Модель «сущность-связь».",
    answer:
      "Модель «сущность-связь» отображает сущности, их атрибуты и связи между ними. Сущности представлены прямоугольниками, а связи - линиями с кардинальностями.",
  },
  {
    question: "Сущности, атрибуты, связи. Сущности-связи и мощности связей.",
    answer:
      "Сущности - объекты, атрибуты - их характеристики, связи - взаимоотношения между сущностями. Мощность связи определяет количество связанных объектов.",
  },
  {
    question:
      "Технология физического проектирования. Основные этапы и их характеристика.",
    answer:
      "Физическое проектирование привязывает структуру данных к конкретной технологии. Этапы: определение структуры хранения, оптимизация запросов, создание индексов и пр.",
  },
  {
    question: "Языковые средства СУБД (DDL, DML, DCL). Общая характеристика.",
    answer:
      "DDL (Data Definition Language) - определение структуры данных. DML (Data Manipulation Language) - манипуляция данными. DCL (Data Control Language) - управление правами доступа.",
  },
  {
    question:
      "Основные понятие и типы сущностей. Обозначение сущностей в различных нотациях. Привести примеры сущностей. Понятие и типы связей. Обозначение связей в различных нотациях. Привести примеры связей.",
    answer:
      "Сущности - объекты в системе. Примеры: Сотрудник, Заказ, Товар. Типы связей: один к одному, один ко многим, многие ко многим. Примеры обозначений: Черта, Крест, Ромб.",
  },
  {
    question: "Основные типы данных (на примере конкретной(ых) СУБД).",
    answer:
      "Типы данных могут включать целые числа, числа с плавающей точкой, строки и даты. Например, в MySQL: INT, VARCHAR, DATE.",
  },
  {
    question:
      "Какие команды относятся к категории DDL? Опишите общий вид синтаксиса команд DDL, приведите пример(ы) каждой команды.",
    answer:
      "Команды DDL (Data Definition Language) отвечают за определение структуры базы данных. Примеры: CREATE TABLE для создания таблицы, ALTER TABLE для изменения структуры таблицы, DROP TABLE для удаления таблицы.",
  },
  {
    question: "Задание ограничений целостности на языке SQL. Примеры.",
    answer:
      "Ограничения целостности могут включать PRIMARY KEY (уникальность идентификатора), FOREIGN KEY (связь между таблицами), CHECK (проверка условия). Пример: CREATE TABLE Employees (ID INT PRIMARY KEY, DepartmentID INT REFERENCES Departments(ID), Salary INT CHECK (Salary > 0)).",
  },
  {
    question:
      "Формирование списка вывода в команде SELECT: общий синтаксис, примеры. Использование псевдонимов в SQL. Упорядочение результата в ответе. Привести примеры.",
    answer:
      "Синтаксис SELECT: SELECT column1, column2 FROM table. Пример с псевдонимом: SELECT FirstName AS 'First Name', LastName AS 'Last Name' FROM Employees. Упорядочение: SELECT * FROM Customers ORDER BY LastName DESC;",
  },
  {
    question:
      "Формирование условия выбора записей в команде SELECT. Использование логических операторов и операторов сравнения. Примеры.",
    answer:
      "Условие выбора: SELECT * FROM Products WHERE Price > 100 AND Category = 'Electronics'. Пример с оператором BETWEEN: SELECT * FROM Orders WHERE OrderDate BETWEEN '2023-01-01' AND '2023-12-31'.",
  },
  {
    question:
      "Использование предикатов в команде SELECT: общий синтаксис, примеры использования (для каждого из предикатов).",
    answer:
      "Предикаты: LIKE, IN, EXISTS, BETWEEN. Примеры: SELECT * FROM Customers WHERE City LIKE 'New%'; SELECT * FROM Products WHERE Category IN ('Electronics', 'Appliances'); SELECT * FROM Orders WHERE EXISTS (SELECT * FROM OrderDetails WHERE OrderDetails.OrderID = Orders.OrderID);",
  },
  {
    question:
      "Группирование данных в SQL. Использование агрегирующих функций для получения сводной информации. Примеры.",
    answer:
      "Группировка: SELECT DepartmentID, COUNT(*) FROM Employees GROUP BY DepartmentID; Агрегирующие функции: SELECT AVG(Salary), MAX(Salary), MIN(Salary) FROM Employees;",
  },
  {
    question:
      "Использование фразы HAVING при группировании данных в SQL. Примеры.",
    answer:
      "HAVING используется для фильтрации результатов группировки. Пример: SELECT DepartmentID, AVG(Salary) FROM Employees GROUP BY DepartmentID HAVING AVG(Salary) > 50000;",
  },
  {
    question: "Вложенные запросы в SQL: типы, примеры по каждому из типов.",
    answer:
      "Вложенные запросы могут быть скалярными (возвращают одно значение), возвращать одну колонку, или таблицу. Примеры: SELECT FirstName FROM Employees WHERE Salary > (SELECT AVG(Salary) FROM Employees); SELECT * FROM Orders WHERE CustomerID IN (SELECT CustomerID FROM Customers WHERE Country = 'USA');",
  },
  {
    question: "Создание и использование представлений в SQL. Примеры.",
    answer:
      "Представления - это виртуальные таблицы, созданные на основе запроса. Пример создания: CREATE VIEW HighSalaries AS SELECT FirstName, LastName FROM Employees WHERE Salary > 100000; Использование: SELECT * FROM HighSalaries;",
  },
  {
    question: "PRIMARY KEY и FOREIGN KEY в языке SQL? Примеры.",
    answer:
      "PRIMARY KEY определяет уникальность идентификатора записи в таблице. Пример: CREATE TABLE Students (StudentID INT PRIMARY KEY, Name VARCHAR(50)); FOREIGN KEY создает связь между таблицами. Пример: CREATE TABLE Orders (OrderID INT PRIMARY KEY, CustomerID INT REFERENCES Customers(CustomerID));",
  },
  {
    question: "Функции для работы с символьными данными в языке SQL.",
    answer:
      "Функции для работы с символьными данными включают: CONCAT (сцепление строк), SUBSTRING (выделение подстроки), UPPER (преобразование в верхний регистр), LOWER (преобразование в нижний регистр), LENGTH (длина строки), и др.",
  },
  {
    question:
      "Назначение инструкции SELECT в языке SQL и логический порядок ее обработки.",
    answer:
      "Инструкция SELECT используется для выборки данных из базы данных. Логический порядок обработки: FROM (определение источников данных), WHERE (фильтрация записей), GROUP BY (группировка данных), HAVING (фильтрация групп), SELECT (выборка столбцов), ORDER BY (сортировка).",
  },
  {
    question:
      "Как выполняется соединение таблиц в языке SQL? Виды соединений. Примеры.",
    answer:
      "Соединение таблиц осуществляется с использованием оператора JOIN. Виды соединений включают INNER JOIN, LEFT JOIN, RIGHT JOIN, и FULL JOIN. Пример: SELECT Employees.FirstName, Departments.DepartmentName FROM Employees INNER JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;",
  },
  {
    question:
      "Подзапрос. Поясните различия между однозначными и многозначными подзапросами, между независимыми и связанными подзапросами.",
    answer:
      "Подзапросы бывают однозначными (возвращают одно значение) и многозначными (возвращают набор значений). Независимый подзапрос может выполняться самостоятельно, а связанный зависит от выполнения внешнего запроса.",
  },
  {
    question: "Операторы манипулирования данными. Примеры.",
    answer:
      "Операторы манипулирования данными включают: INSERT (вставка данных), UPDATE (обновление данных), DELETE (удаление данных). Пример: INSERT INTO Employees (FirstName, LastName) VALUES ('John', 'Doe');",
  },
  {
    question: "Хранимые процедуры. Создание и выполнение.",
    answer:
      "Хранимые процедуры создаются с использованием оператора CREATE PROCEDURE. Выполнение происходит с использованием оператора EXECUTE. Пример создания: CREATE PROCEDURE GetEmployeeCount AS SELECT COUNT(*) FROM Employees;",
  },
  {
    question: "Хранимые процедуры. Параметры в процедурах.",
    answer:
      "Хранимые процедуры могут иметь входные и выходные параметры. Пример с входным параметром: CREATE PROCEDURE GetEmployeeByDepartment (IN departmentID INT) AS SELECT * FROM Employees WHERE DepartmentID = departmentID;",
  },
  {
    question: "Функции. Синтаксис. Виды.",
    answer:
      "Функции в языке SQL могут быть встроенными (например, AVG, COUNT) или пользовательскими. Синтаксис: SELECT AVG(Salary) FROM Employees; Виды: агрегатные, строковые, числовые и др.",
  },
  {
    question: "Триггеры. Синтаксис. Виды.",
    answer:
      "Триггеры в языке SQL выполняются автоматически при определенных событиях (INSERT, UPDATE, DELETE). Синтаксис: CREATE TRIGGER triggerName ON tableName FOR INSERT AS ... Виды: BEFORE и AFTER триггеры.",
  },
  {
    question:
      "Определение прав доступа пользователей к данным. Стандартные привилегии.",
    answer:
      "Определение прав доступа включает GRANT (предоставление прав) и REVOKE (отзыв прав). Стандартные привилегии включают SELECT (чтение данных), INSERT (вставка данных), UPDATE (обновление данных), DELETE (удаление данных) и др.",
  },
]);

const activeQuestionIdx = ref(0);

const question = computed(() => {
  return questions.value[activeQuestionIdx.value];
});

const nextQuestion = () => {
  if (activeQuestionIdx.value === questions.value.length - 1) {
    activeQuestionIdx.value = 0;
  } else {
    activeQuestionIdx.value++;
  }
};

const prevQuestion = () => {
  if (activeQuestionIdx.value === 0) {
    activeQuestionIdx.value = questions.value.length - 1;
  } else {
    activeQuestionIdx.value--;
  }
};
</script>

<style lang="scss" scoped>
.v-enter-active,
.v-leave-active {
  transition: opacity 0.2s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
.main {
  height: 100vh;
  width: 100vw;
}

#modal,
#overlay {
  transition: opacity 0.2s;
}

.hide {
  opacity: 0;
  pointer-events: none;
}
</style>
