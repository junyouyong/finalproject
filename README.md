# CS50 Final Project: Tuition50

Tuition50 is ...


## Usage

**Registration**

Students are required to sign up in order to access the tuition matching algorithm that matches them to their desired tutor.
Tutors, however, do not need to sign up as they are only required to list their services in a form.

**Log in**

....

**Tutor Profiles**

....

**Request for tutor**

....

**Write a testimonial**

....

**Testimonials**

....



## Algorithms

**Matching students to tutors**

We will search the database for the desired qualities that a student requires from his/her tutor and provide a match to the student.
The student will then be able to email the tutor to arrange a session with the tutor.

```
def request_tutor():
    if request.method == "POST":
        level = request.form.get("level")
        subject = request.form.get("subject")
        gender = request.form.get("gender preferences")
        qualifications = request.form.get("qualifications of tutor")
        row = db.execute("SELECT * FROM tutors WHERE gender=:gender AND level=:level AND subject=:subject AND qualifications=:qualifications",
                           gender=gender, level=level, subject=subject, qualifications=qualifications)
        if len(row) == 0:
            flash("No Match!")
            return render_template("request_tutor.html")
        return render_template("requested.html", row = row)
    else:
        return render_template("request_tutor.html")
```



**Posting a testimonial**

When the student submits his/her testimonial, the testimonial will be recorded in our database and reflected in the list of testimonials
containing all the tutors' testimonials.

```
def testimonial():
    if request.method == "POST":
        tutor_name = request.form.get("tutor")
        testimonial = request.form.get("description")
        student_id = session["user_id"]
        db.execute("INSERT INTO testimonial (student_id, tutor_name, testimonial) VALUES (:student_id, :tutor_name, :testimonial)",
                    student_id=student_id, tutor_name=tutor_name, testimonial=testimonial)
        flash("Success")
        return render_template("testimonials.html")
    else:
        row = db.execute("SELECT * FROM tutors")
        return render_template("testimonial.html", row = row)
```
