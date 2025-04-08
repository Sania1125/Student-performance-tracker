# Student performance tracker

class Student:
    def __init__(self, name, roll, marks):
        self.name = name
        self.roll = roll
        self.marks = marks  # Dictionary: subject: score
        self.total = sum(marks.values())
        self.percentage = round(self.total / len(marks), 2)
        self.grade = self.calculate_grade()

    def calculate_grade(self):
        if self.percentage >= 90:
            return "A+"
        elif self.percentage >= 80:
            return "A"
        elif self.percentage >= 70:
            return "B"
        elif self.percentage >= 60:
            return "C"
        else:
            return "Fail"

    def __str__(self):
        return f"{self.name} ({self.roll}) | {self.percentage}% | Grade: {self.grade}"


class ResultDashboard:
    def __init__(self):
        self.students = []

    def add_student(self, student):
        self.students.append(student)

    def view_all(self):
        print("\n📋 All Student Results:")
        for s in self.students:
            print(s)

    def search_by_roll(self, roll):
        for s in self.students:
            if s.roll == roll:
                print("\n🎯 Student Found:")
                print(s)
                return
        print("❌ No student found with this roll number.")

    def calculate_class_average(self):
        if not self.students:
            print("No data.")
            return
        avg = round(sum(s.percentage for s in self.students) / len(self.students), 2)
        print(f"\n📊 Class Average Percentage: {avg}%")

    def find_topper(self):
        if not self.students:
            print("No data.")
            return
        topper = max(self.students, key=lambda s: s.percentage)
        print(f"\n🏆 Class Topper: {topper.name} ({topper.percentage}%)")


# Example usage
if __name__ == "__main__":
    dashboard = ResultDashboard()

    # Adding students
    s1 = Student("Ahsan", "BSM-23-01", {"Math": 90, "English": 85, "Physics": 88})
    s2 = Student("Zara", "BSM-23-02", {"Math": 70, "English": 78, "Physics": 72})
    s3 = Student("Usman", "BSM-23-03", {"Math": 95, "English": 90, "Physics": 92})

    dashboard.add_student(s1)
    dashboard.add_student(s2)
    dashboard.add_student(s3)

    dashboard.view_all()
    dashboard.search_by_roll("BSM-23-02")
    dashboard.calculate_class_average()
    dashboard.find_topper()

