# CS50 Final Project: Tuition50

Tuition50 is ...

## Usage

**Registration**

Students are required to sign up in order to access the tuition matching algorithm that matches them to their desired tutor.
Tutors, however, do not need to sign up as they are only required to list their services in a form.

**

## Algorithms

**Matching students to tutors**

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
