# dynamic-form-handling-react-js-code


import React, { useState } from "react";

const DynamicForm = () => {
  const [formFields, setFormFields] = useState([{ trainer: "", course: "" }]);
  const [submittedData, setSubmittedData] = useState(null);

  const trainers = [
    { trainerName: "Trainer 1", trainerId: 1 },
    { trainerName: "Trainer 2", trainerId: 2 },
    { trainerName: "Trainer 3", trainerId: 3 },
  ];

  const courses = [
    { courseName: "Course 1", courseId: 1, trainerId: 1 },
    { courseName: "Course 2", courseId: 2, trainerId: 1 },
    { courseName: "Course 3", courseId: 3, trainerId: 2 },
    { courseName: "Course 4", courseId: 4, trainerId: 2 },
    { courseName: "Course 5", courseId: 5, trainerId: 3 },
  ];

  const handleTrainerChange = (index, trainerId) => {
    const updatedFormFields = [...formFields];
    updatedFormFields[index].trainer = trainerId;
    setFormFields(updatedFormFields);
  };

  const handleCourseChange = (index, courseId) => {
    const updatedFormFields = [...formFields];
    updatedFormFields[index].course = courseId;
    setFormFields(updatedFormFields);
  };

  const handleAddField = () => {
    setFormFields([...formFields, { trainer: "", course: "" }]);
  };

  const handleRemoveField = (index) => {
    const updatedFormFields = [...formFields];
    updatedFormFields.splice(index, 1);
    setFormFields(updatedFormFields);
  };

  const handleSubmit = () => {
    // Save the submitted data
    setSubmittedData([...formFields]);
  };

  return (
    <div>
      {formFields.map((field, index) => (
        <div key={index}>
          {/* Trainer dropdown */}
          <label>
            Select Trainer:
            <select
              value={field.trainer}
              onChange={(e) => handleTrainerChange(index, e.target.value)}
            >
              <option value="">Select Trainer</option>
              {trainers.map((trainer) => (
                <option key={trainer.trainerId} value={trainer.trainerId}>
                  {trainer.trainerName}
                </option>
              ))}
            </select>
          </label>

          {/* Course dropdown */}
          <label>
            Select Course:
            <select
              value={field.course}
              onChange={(e) => handleCourseChange(index, e.target.value)}
            >
              <option value="">Select Course</option>
              {courses.map(
                (course) =>
                  course.trainerId === parseInt(field.trainer, 10) && (
                    <option key={course.courseId} value={course.courseId}>
                      {course.courseName}
                    </option>
                  )
              )}
            </select>
          </label>

          {/* Remove button */}
          {index > 0 && (
            <button type="button" onClick={() => handleRemoveField(index)}>
              Remove
            </button>
          )}
        </div>
      ))}

      {/* Add button */}
      <button type="button" onClick={handleAddField}>
        Add Field
      </button>

      {/* Submit button */}
      <button type="button" onClick={handleSubmit}>
        Submit
      </button>

      {/* Display submitted data */}
      {submittedData && (
        <div>
          <h2>Submitted Data:</h2>
          <pre>{JSON.stringify(submittedData, null, 2)}</pre>
        </div>
      )}
    </div>
  );
};

export default DynamicForm;
