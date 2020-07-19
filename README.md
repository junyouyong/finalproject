# CS50 Final Project: Tuition50

Tuition50 is a website that offers academic help to students by allowing them to find suitable tutors that match their preferences.
OUr target audience are students studying in secondary schools and junior colleges.
We allow tutors to advertise their services by filling up a form to indicate their qualifications and the subject they teach.
Their profiles are listed for interested students to view.
To ensure that students can find a suitable tutor that meets their preferences, students can fill up a form to request for a tutor.
We match students to tutors that meet their requirements and they will be provided with the tutor's email to contact them for their services.

## Usage

**Registration**

Students are required to sign up in order to access the tuition matching algorithm that matches them to their desired tutor.
Tutors, however, do not need to sign up as they are only required to list their services in a form.

**Log in**

....

**Tutor Profiles**
Tutors who signed up will have their profiles listed for students to view. Profiles include their age, gender, qualifications and the subject they teach.
....

**Request for tutor**
Students interested to find a tutor for a particular subject can fill up the tutor request form where they will specify their preferences like gender and qualifications of the tutor.
After that, we match the student's preferences with tutors whose profile match their specifications.
....

**Write a testimonial**
Our website provide a platform for students to share their tutoring experience with a particular tutor listed on the website.
Students have to specify the tutor name while writing the testimonial and we ensure that they can only write testimonials for tutors that have been listed on our website and that no blank description are submitted.
....

**Testimonials**
This is a page that displays testimonials written by students regarding their experience with a particular tutor.
....

**Tutor Rates**

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

