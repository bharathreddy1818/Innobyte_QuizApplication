# Online Quiz Application

A desktop quiz application written in Java (Swing) with a SQLite database accessed through JDBC. Users register, log in and take a timed multiple-choice quiz. Administrators manage the question bank from a separate admin panel.

## Features

- **User authentication:** registration and login for users
- **Separate admin login:** administrators use a dedicated login and admin panel
- **Password security:** passwords are salted and hashed with PBKDF2 (HmacSHA256) before storage, so no plain-text passwords are kept
- **Admin panel:** add questions (text, four options, correct answer), view all questions, and delete questions or users
- **Quiz taking:** questions are shown one at a time with four options
- **Timer:** the quiz is limited to 10 minutes and ends automatically when time runs out
- **Scoring:** the final score is displayed at the end of the quiz
- **Persistence:** users and questions are stored in `QuizDB.db` (SQLite) using JDBC with `PreparedStatement`s

## Tech Stack

| Component | Technology |
|---|---|
| Language | Java 11+ |
| UI | Java Swing |
| Database | SQLite |
| Database access | JDBC (`sqlite-jdbc`) |

## Project Structure

```
quiz-application/
├── src/org/quiz_application/
│   ├── ProfileChooser.java  # Main class: choose Admin or User
│   ├── AdminLogin.java      # Admin login
│   ├── AdminPanel.java      # Add / view / delete questions and users
│   ├── UserLogin.java       # User login
│   ├── Register.java        # User registration
│   ├── Quiz.java            # Quiz screen, timer and scoring
│   ├── Question.java        # Question model
│   └── DataBase.java        # JDBC access and password hashing
├── lib/                     # sqlite-jdbc jar goes here
├── QuizDB.db                # SQLite database
└── README.md
```

## Setup Instructions

### Prerequisites
- JDK 11 or higher (check with `java -version`)
- The SQLite JDBC driver jar from the [xerial/sqlite-jdbc releases](https://github.com/xerial/sqlite-jdbc/releases), placed in the `lib/` folder

### Run in an IDE
1. Clone the repository:
```bash
   git clone https://github.com/bharathreddy1818/Innobyte_QuizApplication.git
```
2. Open the `quiz-application` folder as a project in NetBeans, IntelliJ or Eclipse.
3. Add the jar(s) from `lib/` to the project libraries.
4. Run the main class `ProfileChooser`. Run it from the project root so that `QuizDB.db` is found.

### Run from the command line
```bash
cd quiz-application
javac -cp "lib/*" -d out src/org/quiz_application/*.java
java -cp "out:lib/*" org.quiz_application.ProfileChooser
```
On Windows, use `;` instead of `:` in the classpath (`out;lib/*`).

### Default Admin Login
- Username: `Admin`
- Password: `1234`

## User Guide

**User**
1. Start the app and choose **User**.
2. Click **Register** and enter a numeric User ID, name, email and password.
3. Log in with your User ID and password.
4. Select one answer per question and click **Next**.
5. Your score is shown at the end of the quiz, or when the timer runs out.

**Administrator**
1. Start the app and choose **Admin**, then log in.
2. Enter the question, the four options, and the correct answer. Type the answer exactly as it appears in one of the options.
3. Click **Add Question**. Use **View All Questions** to see what is stored.
4. To delete, choose `question` or `users` in the dropdown, enter the ID, and click **Remove**.

## Database

| Table | Columns |
|---|---|
| `users` | userID, username, email, password (stored as `salt:hash`) |
| `question` | QuestionID, Question, Option1–4, Answer |

## Assumptions

- User IDs are numeric and unique.
- Each question has four options and exactly one correct answer.
- The application runs locally on a single machine using a local SQLite file.

## Limitations

- All questions share one pool: there are no separate quizzes or topics.
- Questions cannot be edited in place; delete and re-add them.
- Only single-answer questions are supported.
- The score is shown only at the end; there is no per-question feedback.
- Quiz attempts are not saved, so past attempts cannot be viewed.
- The admin credentials are hard-coded in the source code.
- No password reset, leaderboard, random question order or difficulty levels.

## Future Improvements

- Quiz topics and difficulty levels
- Immediate correct/incorrect feedback after each question
- Saving and viewing past quiz attempts
- Editing questions and supporting multiple correct answers
- Leaderboard
- Storing admin accounts in the database

## Development Notes

This project is based on the open-source *Quiz Application* tutorial by ProjectGurukul. Changes made during the internship:
- Added password hashing with a random salt (PBKDF2)
- Renamed the package to `org.quiz_application` and updated the window titles
- Added this documentation

## Author

**Bharath Kumar**
GitHub: [bharathreddy1818](https://github.com/bharathreddy1818)
