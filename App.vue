<template>
  <div class="bg-gray-50 text-gray-800">
    <!-- Section 1: Paper Title and Abstract -->
    <section class="max-w-4xl mx-auto mt-16 p-8 bg-white rounded-2xl shadow-md mb-10">
      <div class="flex justify-center items-center gap-4 mb-4">
        <h1 class="text-3xl font-bold text-blue-600">{{ title }}</h1>
        <img src="./images/speech_icon.png" alt="Speech Communication Icon" class="w-20 h-20 object-contain">
      </div>
      <p class="text-lg mb-6 italic text-center">{{ subtitle }}</p>
      
      <h2 class="text-xl font-semibold mb-3 text-gray-800">Abstract</h2>
      <p class="text-base leading-relaxed text-gray-700 mb-6">
        This project introduces <strong>UnspokenBench</strong>, a bilingual benchmark designed to evaluate the metaphorical reasoning abilities of Audio Language Models (ALMs). It focuses on audio-specific cues like prosody, emotional tone, and phonetic ambiguity, which are critical for understanding non-literal meaning. Through carefully constructed Q&A tasks, we explore how well current models grasp implied content in spoken language, especially in metaphorical and humorous contexts.
      </p>
      
      <div class="mt-4">
        <h2 class="text-xl font-semibold mb-3 text-gray-800">Key Words</h2>
        <p class="text-gray-700">
          <span v-for="(keyword, index) in keywords" :key="index">
            <em><strong>{{ keyword }}</strong></em>{{ index < keywords.length - 1 ? ', ' : '' }}
          </span>
        </p>
      </div>
    </section>

    <!-- Section 2: Question Examples -->
    <section class="max-w-4xl mx-auto p-8 bg-white rounded-2xl shadow-md mb-16">
      <h2 class="text-2xl font-semibold mb-4 text-blue-600">Question Examples</h2>

      <div v-for="(question, index) in questions" :key="index" class="mb-10">
        <p class="mb-3 font-medium">Question {{ index + 1 }}:</p>
        <p class="mb-6">{{ question.text }}</p>
        <audio controls class="w-full mb-4">
          <source :src="question.audioSrc" type="audio/mpeg">
          Your browser does not support the audio element.
        </audio>
        <div class="space-y-2 text-gray-700">
          <p v-for="(option, optIndex) in question.options" :key="optIndex" 
             :class="{'flex items-center gap-2': option.isCorrect}">
            <u v-if="option.isCorrect">{{ option.text }}</u>
            <span v-else>{{ option.text }}</span>
            <img v-if="option.isCorrect" src="./images/right.png" alt="Correct" class="w-6 h-6">
          </p>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
const title = 'Listening Between the Lines'
const subtitle = 'Evaluating Metaphorical Reasoning in Audio Language Models'

const keywords = [
  'Audio Language Models',
  'Metaphorical Reasoning',
  'Prosody Analysis',
  'Natural Language Processing',
  'Speech Understanding'
]

const questions = [
  {
    text: 'What is the implied meaning when the speaker says "it\'s raining cats and dogs"?',
    audioSrc: './samples/rain.mp3',
    options: [
      { text: 'A. It\'s raining very heavily', isCorrect: true },
      { text: 'B. Animals are falling from the sky', isCorrect: false },
      { text: 'C. The weather is unpredictable', isCorrect: false },
      { text: 'D. The speaker is exaggerating', isCorrect: false },
      { text: 'E. There\'s a pet parade happening', isCorrect: false }
    ]
  },
  {
    text: 'How does the speaker\'s tone change when saying "I\'m over the moon"?',
    audioSrc: './samples/moon.mp3',
    options: [
      { text: 'A. Tone becomes higher and more excited', isCorrect: true },
      { text: 'B. Tone becomes lower and more serious', isCorrect: false },
      { text: 'C. Tone remains neutral throughout', isCorrect: false },
      { text: 'D. Tone becomes sarcastic', isCorrect: false },
      { text: 'E. Tone fluctuates unpredictably', isCorrect: false }
    ]
  },
  {
    text: 'What emotion is conveyed when the speaker says "my heart sank"?',
    audioSrc: './samples/heart.mp3',
    options: [
      { text: 'A. Disappointment', isCorrect: true },
      { text: 'B. Surprise', isCorrect: false },
      { text: 'C. Happiness', isCorrect: false },
      { text: 'D. Anger', isCorrect: false },
      { text: 'E. Confusion', isCorrect: false }
    ]
  },
  {
    text: 'What is the humorous intent behind "that joke was so bad it\'s good"?',
    audioSrc: './samples/joke.mp3',
    options: [
      { text: 'A. The joke is intentionally terrible', isCorrect: false },
      { text: 'B. The speaker doesn\'t understand the joke', isCorrect: false },
      { text: 'C. The humor comes from the absurdity', isCorrect: true },
      { text: 'D. The joke is actually clever', isCorrect: false },
      { text: 'E. The speaker is being sarcastic', isCorrect: false }
    ]
  },
  {
    text: 'How does the speaker emphasize the phrase "time flies when you\'re having fun"?',
    audioSrc: './samples/time.mp3',
    options: [
      { text: 'A. By speaking faster', isCorrect: false },
      { text: 'B. By pausing before the phrase', isCorrect: false },
      { text: 'C. By changing pitch', isCorrect: true },
      { text: 'D. By repeating the phrase', isCorrect: false },
      { text: 'E. By using hand gestures (implied in tone)', isCorrect: false }
    ]
  }
]
</script>