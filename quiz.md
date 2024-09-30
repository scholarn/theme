---
layout: default
title: Mock Test
---

<h1>Mock Test</h1>

<form id="quiz-form">
  {% for q in site.data.quiz.quiz %}
    <h3>{{ q.question }}</h3>
    {% for option in q.options %}
      <input type="radio" name="question_{{ forloop.index }}" value="{{ option }}"> {{ option }}<br>
    {% endfor %}
    <br>
  {% endfor %}
  <input type="submit" value="Submit">
</form>

<div id="result"></div>

<script>
  document.getElementById("quiz-form").onsubmit = function(e) {
    e.preventDefault();
    let score = 0;
    let correctAnswers = {{ site.data.quiz.quiz | jsonify }};
    
    correctAnswers.forEach((question, index) => {
      let selectedOption = document.querySelector(`input[name="question_${index + 1}"]:checked`);
      if (selectedOption && selectedOption.value === question.correct) {
        score++;
      }
    });

    document.getElementById("result").innerHTML = `Your score: ${score}/${correctAnswers.length}`;
  };
</script>
