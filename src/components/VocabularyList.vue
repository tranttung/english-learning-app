<!-- src/components/VocabularyList.vue -->
<template>
    <h2>{{ title }}</h2>
    <div>
        <ul>
        <li v-for="(item, index) in words" :key="index">
            <div>
            <strong style="width: 100px;">{{ item.translation }}</strong>
            <button @click="speakWord(item.word)">Nghe</button>
            </div>
            <input v-model="userAnswers[index]" placeholder="Nhập từ bạn nghe được" />
            <button @click="checkAnswer(index, item.word)">Kiểm tra</button>
            <span v-if="feedback[index]" :class="feedback[index].class">
            {{ feedback[index].message }}
            </span>
        </li>
        </ul>
    </div>
</template>

<script>
export default {
  props: {
    title: String,
    words: Array,
  },
  data() {
    return {
      userAnswers: [], // Lưu câu trả lời của người dùng
      feedback: [], // Lưu phản hồi cho từng từ
    };
  },
  methods: {
    speakWord(word) {
      const utterance = new SpeechSynthesisUtterance(word);
      utterance.lang = "en-US";
      speechSynthesis.speak(utterance);
    },
    checkAnswer(index, correctWord) {
      const userAnswer = this.userAnswers[index]?.trim().toLowerCase();
      const isCorrect = userAnswer === correctWord.toLowerCase();
      this.feedback[index] = {
        message: isCorrect ? "Đúng!" : "Sai, thử lại.",
        class: isCorrect ? "correct" : "incorrect",
      };
    },
  },
};
</script>

<style scoped>
.correct {
  color: green;
}
.incorrect {
  color: red;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 10px 0;
  display: flex;
  align-items: center;
}
div {
  display: flex;
  align-items: center;
  margin-right: 10px;
}
button {
  margin-left: 10px;
  padding: 8px 12px;
  background-color: #3498db;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
button:hover {
  background-color: #2980b9;
}
input {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-left: 10px;
  min-width: 200px;
}
</style>

