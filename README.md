import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("bd_students_per_v2.csv")
df["AttendancePercentage"] = df["attendance"]

def categorize_attendance(pct):
    if pct >= 75:
        return "Good"
    elif pct >= 50:
        return "Average"
    else:
        return "Poor"

df["Category"] = df["AttendancePercentage"].apply(categorize_attendance)

print("Attendance Summary:")
print(df["AttendancePercentage"].describe())
print("\nCategory Counts:")
print(df["Category"].value_counts())

plt.figure(figsize=(8, 5))
df["Category"].value_counts().plot(kind="bar", color=["green", "orange", "red"])
plt.title("Attendance Categories")
plt.xlabel("Category")
plt.ylabel("Number of Students")
plt.xticks(rotation=0)
plt.tight_layout()
plt.show()

plt.figure(figsize=(6, 6))
df["Category"].value_counts().plot(kind="pie", autopct="%1.1f%%", colors=["green","orange","red"])
plt.title("Attendance Distribution")
plt.ylabel("")
plt.tight_layout()
plt.show()

df.to_csv("attendance_analyzed.csv", index=False)
