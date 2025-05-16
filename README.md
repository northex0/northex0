## Hi there 👋

<!--
**northex0/northex0** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
# تثبيت المكتبات
!pip install --upgrade gspread pandas matplotlib seaborn

# استيراد المكتبات
import pandas as pd
import gspread
from google.colab import auth
from google.auth import default
import matplotlib.pyplot as plt
import seaborn as sns

# تسجيل الدخول وتفويض
auth.authenticate_user()
creds, _ = default()
gc = gspread.authorize(creds)

# ضع رابط Google Sheet الخاص بك هنا
SHEET_URL = https://docs.google.com/spreadsheets/d/1SI8UJuOCOV4ctH-CO7AKMY2ckSPwCapBHKUJ3kRUmRk/edit?usp=drivesdk

# فتح ملف جوجل شيت
sheet = gc.open_by_url(SHEET_URL)
worksheet = sheet.sheet1
data = worksheet.get_all_records()
df = pd.DataFrame(data)

# عرض عينة من البيانات
print("عينة من البيانات:")
display(df.head())

# ========== تحليل الأنياجرام ==========
def analyze_enneagram(df):
    # افتراض: العمود 'Enneagram Type' يحتوي على النوع (1-9)
    if 'Enneagram Type' in df.columns:
        counts = df['Enneagram Type'].value_counts().sort_index()
        print("\nتوزيع الأنياجرام:")
        print(counts)
        plt.figure(figsize=(8,4))
        sns.barplot(x=counts.index, y=counts.values, palette='coolwarm')
        plt.title('توزيع الأنياجرام')
        plt.xlabel('نوع الأنياجرام')
        plt.ylabel('عدد المشاركين')
        plt.show()
    else:
        print("لا يوجد عمود 'Enneagram Type' في البيانات.")

# ========== تحليل MBTI ==========
def analyze_mbti(df):
    # افتراض: العمود 'MBTI Type' يحتوي على النمط
    if 'MBTI Type' in df.columns:
        counts = df['MBTI Type'].value_counts().sort_index()
        print("\nتوزيع MBTI:")
        print(counts)
        plt.figure(figsize=(12,5))
        sns.barplot(x=counts.index, y=counts.values, palette='magma')
        plt.title('توزيع أنماط MBTI')
        plt.xlabel('نوع MBTI')
        plt.ylabel('عدد المشاركين')
        plt.xticks(rotation=45)
        plt.show()
    else:
        print("لا يوجد عمود 'MBTI Type' في البيانات.")

# ========== تحليل الوظائف المعرفية MBTI ==========
def analyze_cognitive_functions(df):
    # افتراض: الأعمدة تحمل أسماء الوظائف المعرفية مثل 'Ti', 'Ne', 'Si', 'Fe'...
    cognitive_funcs = ['Ti', 'Te', 'Fi', 'Fe', 'Si', 'Se', 'Ni', 'Ne']
    present_funcs = [col for col in cognitive_funcs if col in df.columns]
    if present_funcs:
        print("\nإحصائيات الوظائف المعرفية MBTI:")
        display(df[present_funcs].describe())
        plt.figure(figsize=(10,6))
        sns.boxplot(data=df[present_funcs])
        plt.title('مقارنة الوظائف المعرفية')
        plt.show()
    else:
        print("لا توجد أعمدة للوظائف المعرفية في البيانات.")

# ========== تحليل DISC ==========
def analyze_disc(df):
    # افتراض: الأعمدة 'D', 'I', 'S', 'C' تمثل الدرجات
    disc_cols = ['D', 'I', 'S', 'C']
    present_disc = [col for col in disc_cols if col in df.columns]
    if present_disc:
        print("\nإحصائيات DISC:")
        display(df[present_disc].describe())
        plt.figure(figsize=(10,6))
        sns.boxplot(data=df[present_disc])
        plt.title('تحليل DISC')
        plt.show()
    else:
        print("لا توجد أعمدة DISC في البيانات.")

# ========== تحليل الظل ==========
def analyze_shadow(df):
    # افتراض: الأعمدة للوظائف المعرفية في نموذج الظل تبدأ بـ 'Shadow_'
    shadow_cols = [col for col in df.columns if col.startswith('Shadow_')]
    if shadow_cols:
        print("\nإحصائيات تحليل الظل:")
        display(df[shadow_cols].describe())
        plt.figure(figsize=(10,6))
        sns.boxplot(data=df[shadow_cols])
        plt.title('تحليل الظل')
        plt.show()
    else:
        print("لا توجد أعمدة لتحليل الظل في البيانات.")

# ========== تشغيل التحليلات ==========
analyze_enneagram(df)
analyze_mbti(df)
analyze_cognitive_functions(df)
analyze_disc(df)
analyze_shadow(df)
