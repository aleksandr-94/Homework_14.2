# Homework_14.2



class Student:
    def __init__(self, gender, age, first_name, last_name, record_book):
        self.gender = gender
        self.age = age
        self.first_name = first_name
        self.last_name = last_name
        self.record_book = record_book

    def __str__(self):
        return f"{self.first_name} {self.last_name}, {self.age} years old, {self.gender}, Record Book: {self.record_book}"

    def __hash__(self):
        return hash(str(self))

    def __eq__(self, other):
        if not isinstance(other, Student):
            return False
        return (
            self.first_name == other.first_name and
            self.last_name == other.last_name and
            self.record_book == other.record_book
        )




class Group:
    def __init__(self, number):
        self.number = number
        self.students = set()

    def add_student(self, student):
        if len(self.students) >= 10:
            raise ValueError("Cannot add more than 10 students to the group!")
        self.students.add(student)

    def delete_student(self, last_name):
        student_to_remove = self.find_student(last_name)
        if student_to_remove:
            self.students.remove(student_to_remove)

    def find_student(self, last_name):
        for student in self.students:
            if student.last_name == last_name:
                return student
        return None

    def __str__(self):
        students_info = "\n".join([str(student) for student in self.students])
        return f"Group: {self.number}\nStudents:\n{students_info}"




from student import Student
from group import Group

if __name__ == "__main__":
    st1 = Student('Male', 30, 'Steve', 'Jobs', 'AN142')
    st2 = Student('Female', 25, 'Liza', 'Taylor', 'AN145')

    gr = Group('PD1')
    gr.add_student(st1)
    gr.add_student(st2)

    print(gr)

    assert gr.find_student('Jobs') == st1
    assert gr.find_student('Jobs2') is None

    gr.delete_student('Taylor')
    print(gr)  # Only one student

    try:
        for _ in range(10):
            gr.add_student(Student('Gender', 20, 'First', 'Last', 'RB123'))
    except ValueError as e:
        print(e)  # Exception: Cannot add more than 10 students
