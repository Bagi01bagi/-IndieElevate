import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Загрузка данных из файла CSV
data = pd.read_csv(r'C:\Users\Adm\Downloads\data (1).csv', encoding='utf-8')
# Проверка структуры данных
print(data.head())  # Вывод первых 5 строк данных

C:\MyPythonProjects\pythonProject3_tz\.venv\Scripts\python.exe C:\MyPythonProjects\pythonProject3_tz\main.py 
  applicant_name   Age   Ответ на вопрос
0         name_0  49.0               нет
1         name_1  37.0                да
2         name_2  18.0               нет
3         name_3  36.0  неверное решение
4         name_4  31.0                да

# Преобразование столбца 'Ответ на вопрос' в бинарный формат (1 - да, 0 - нет, NaN - игнорировать)
data['Ответ на вопрос'] = data['Ответ на вопрос'].map({'да': 1, 'нет': 0})

# Удаление строк с пропущенными значениями в столбце 'Age' или 'Ответ на вопрос'
data = data.dropna(subset=['Age', 'Ответ на вопрос'])

# Группировка данных по возрасту и подсчет доли соискателей с решением задачи
age_solution_ratio = data.groupby('Age')['Ответ на вопрос'].mean().reset_index()

# Построение графика
plt.figure(figsize=(10, 6))
sns.barplot(data=age_solution_ratio, x='Age', y='Ответ на вопрос', hue='Age', palette='viridis', legend=False)
plt.title('Доля соискателей с решением задачи по возрасту')
plt.xlabel('Возраст')
plt.ylabel('Доля с решением задачи')
plt.xticks(rotation=45)
plt.grid(axis='y')
plt.tight_layout()

# Сохранение графика (опционально)
plt.savefig('age_solution_ratio.png')

# Показать график
plt.show()

![Image alt](https://github.com/{username}/{repository}/raw/{branch}/{path}/image.png)

plt.figure(figsize=(10, 6))
sns.histplot(data=age_solution_ratio, x='Age', weights='Ответ на вопрос', kde=True, color='b')
plt.title('Доля соискателей с решением задачи по возрасту (гистограмма)')
plt.xlabel('Возраст')
plt.ylabel('Доля с решением задачи')
plt.xticks(rotation=45)
plt.xlim(0, 100)  # Ограничиваем возраст до 100 лет
plt.tight_layout()

plt.savefig('age_solution_ratio_hist.png')
plt.show()
![Image alt](https://github.com/{username}/{repository}/raw/{branch}/{path}/image.png)
