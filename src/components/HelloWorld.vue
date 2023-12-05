<script setup lang="ts">
  // Import types or define them here
  import { ref } from 'vue';
  import { onMounted } from 'vue'

  interface QuestionOption {
  [key: number]: {
    optionText: string;
    scores: {
      DFW: number;
      Pascal: number;
      Plato: number;
      Aristotle: number;
      Seneca: number;
      Sartre: number;
      Crawford: number;
    };
  };
}


  interface QuizQuestion {
    id: number;
    question: string;
    options: QuestionOption;
  }

/*  interface UserResponses {
    [key: number]: {
      rating: number;
    };
  } */
  interface UserResponses {
    [key: number]: {
      rating: number | null; // Allow null for initial state
    } | undefined; // Allow undefined for initial state
  }

  // Declare reactive variables
  const quizQuestions: QuizQuestion[] = [
  {
    id: 1,
    question: "Friends who ask you favors all the time are NOT worthwhile.",
    options: {
      1: {
        optionText: "True",
        scores: {
          DFW: 5,
          Pascal: 6,
          Plato: 3,
          Aristotle: 4,
          Seneca: 10,
          Sartre: 7,
          Crawford: 5
        }
      },
      2: {  
        optionText: "False"
        }
  }
  },
  {
    id: 2,
    question: "What is a friendship most useful for?",
    options: {
      1: {
        optionText: "Making decisions",
        scores: {
          DFW: 7,
          Pascal: 5,
          Plato: 9,
          Aristotle: 8,
          Seneca: 4,
          Sartre: 1,
          Crawford: 7
        }
      },
      2: {
        optionText: "Helping with menial personal tasks",
        scores: {
          DFW: 4,
          Pascal: 7,
          Plato: 4,
          Aristotle: 3,
          Seneca: 1,
          Sartre: 5,
          Crawford: 3
        }
      },
      3: {
        optionText: "Having fun together",
        scores: {
          DFW: 4,
          Pascal: 8,
          Plato: 5,
          Aristotle: 3,
          Seneca: 10,
          Sartre: 5,
          Crawford: 6
        }
      },
      4: {
        optionText: "Working together on a job",
        scores: {
          DFW: 5,
          Pascal: 9,
          Plato: 9,
          Aristotle: 8,
          Seneca: 2,
          Sartre: 5,
          Crawford: 10
        }
      }
    }
  },
  {
    id: 3,
    question: "Focusing on yourself is always better than focusing on others.",
    options: {
      1: {
        optionText: "True",
        scores: {
          DFW: 1,
          Pascal: 4,
          Plato: 2,
          Aristotle: 6,
          Seneca: 10,
          Sartre: 8,
          Crawford: 4
        }
      },
      2: {  
        optionText: "False"
        }
    }
  },
  {
    id: 4,
    question: "Mindfulness is...",
    options: {
      1: {
        optionText: "A skill",
        scores: {
          DFW: 0,
          Pascal: 1,
          Plato: 7,
          Aristotle: 7,
          Seneca: 3,
          Sartre: 0,
          Crawford: 5
        }
      },
      2: {
        optionText: "A state of mind",
        scores: {
          DFW: 10,
          Pascal: 9,
          Plato: 3,
          Aristotle: 3,
          Seneca: 7,
          Sartre: 10,
          Crawford: 5
        }
      }
    }
  },
  {
    id: 5,
    question: "In my life, I tend to choose things that make me happy.",
    options: {
      1: {
        optionText: "True",
        scores: {
          DFW: 4,
          Pascal: 8,
          Plato: 5,
          Aristotle: 5,
          Seneca: 6,
          Sartre: 10,
          Crawford: 5
        }
      },
      2: {  
        optionText: "False"
        }
    }
  },
  {
    id: 6,
    question: "The statement 'patience is a virtue' applies to everyone.",
    options: {
      1: {
        optionText: "True",
        scores: {
          DFW: 5,
          Pascal: 0,
          Plato: 7,
          Aristotle: 7,
          Seneca: 2,
          Sartre: 0,
          Crawford: 8
        }
      },
      2: {  
        optionText: "False"
        }
    }
  },
  {
    id: 7,
    question: "Thinking deeply about life will make you happier.",
    options: {
      1: {
        optionText: "True",
        scores: {
          DFW: 3,
          Pascal: 5,
          Plato: 10,
          Aristotle: 9,
          Seneca: 10,
          Sartre: 6,
          Crawford: 3
        }
      },
      2: {  
        optionText: "False"
        }
    }
  },
  {
    id: 8,
    question: "There is such a thing is 'over-thinking' something.",
    options: {
      1: {
        optionText: "True",
        scores: {
          DFW: 9,
          Pascal: 8,
          Plato: 0,
          Aristotle: 1,
          Seneca: 0,
          Sartre: 4,
          Crawford: 3
        }
      },
      2: {  
        optionText: "False"
        }
    }
  },
  {
    id: 9,
    question: "The best teacher is...",
    options: {
      1: {
        optionText: "Yourself",
        scores: {
          DFW: 8,
          Pascal: 4,
          Plato: 3,
          Aristotle: 2,
          Seneca: 8,
          Sartre: 10,
          Crawford: 6
        }
      },
      2: {
        optionText: "Your closest friend(s)",
        scores: {
          DFW: 5,
          Pascal: 6,
          Plato: 7,
          Aristotle: 8,
          Seneca: 5,
          Sartre: 0,
          Crawford: 6
        }
      },
      3: {
        optionText: "Your community",
        scores: {
          DFW: 5,
          Pascal: 6,
          Plato: 7,
          Aristotle: 7,
          Seneca: 5,
          Sartre: 0,
          Crawford: 9
        }
      }
    }
  },
  {
    id: 10,
    question: "Individual thought is better than collective thought.",
    options: {
      1: {
        optionText: "True",
        scores: {
          DFW: 4,
          Pascal: 5,
          Plato: 1,
          Aristotle: 2,
          Seneca: 8,
          Sartre: 10,
          Crawford: 3
        }
      },
      2: {  
        optionText: "False"
        }
    }
  },
  {
    id: 11,
    question: "Learning is useful, regardless of what topic it is.",
    options: {
      1: {
        optionText: "True",
        scores: {
          DFW: 8,
          Pascal: 1,
          Plato: 5,
          Aristotle: 7,
          Seneca: 4,
          Sartre: 0,
          Crawford: 7
        }
      },
      2: {  
        optionText: "False"
        }
    }
  },
  {
    id: 12,
    question: "When I'm not sure about something, it's better to...",
    options: {
      1: {
        optionText: "Go with my gut",
        scores: {
          DFW: 3,
          Pascal: 9,
          Plato: 7,
          Aristotle: 5,
          Seneca: 6,
          Sartre: 10,
          Crawford: 9
        }
      },
      2: {
        optionText: "Do some research",
        scores: {
          DFW: 8,
          Pascal: 1,
          Plato: 5,
          Aristotle: 5,
          Seneca: 3,
          Sartre: 0,
          Crawford: 1
        }
      }
    }
  },
  {
    id: 13,
    question: "What's better for you?",
    options: {
      1: {
        optionText: "One enjoyable all-consuming hobby outside your work",
        scores: {
          DFW: 2,
          Pascal: 8,
          Plato: 5,
          Aristotle: 7,
          Seneca: 10,
          Sartre: 5,
          Crawford: 7
        }
      },
      2: {
        optionText: "A job that used to be your hobby; fun, but you no longer find the same sense of excitement",
        scores: {
          DFW: 5,
          Pascal: 6,
          Plato: 6,
          Aristotle: 3,
          Seneca: 2,
          Sartre: 5,
          Crawford: 10
        }
      },
      3: {
        optionText: "A regular job and regular hobbies",
        scores: {
          DFW: 7,
          Pascal: 2,
          Plato: 4,
          Aristotle: 7,
          Seneca: 5,
          Sartre: 5,
          Crawford: 3
        }
      }
    }
  },
  {
    id: 14,
    question: "I would rather have a job with...",
    options: {
      1: {
        optionText: "Annoying co-workers and 4 weeks paid time off",
        scores: {
          DFW: 3,
          Pascal: 8,
          Plato: 4,
          Aristotle: 7,
          Seneca: 10,
          Sartre: 5,
          Crawford: 0
        }
      },
      2: {
        optionText: "Likeable, friendly co-workers with no paid time off",
        scores: {
          DFW: 7,
          Pascal: 2,
          Plato: 6,
          Aristotle: 3,
          Seneca: 0,
          Sartre: 5,
          Crawford: 10
        }
      }
    }
  },
  {
    id: 15,
    question: "Most 'pleasures' don't make you happy long-term.",
    options: {
      1: {
        optionText: "True",
        scores: {
          DFW: 8,
          Pascal: 9,
          Plato: 10,
          Aristotle: 6,
          Seneca: 1,
          Sartre: 5,
          Crawford: 8
        }
      },
      2: {  
        optionText: "False"
        }
    }
  },
  {
    id: 16,
    question: "I would be better off...",
    options: {
      1: {
        optionText: "Being given a unlimited pass to all sports, amusement parks, and live performances",
        scores: {
          DFW: 3,
          Pascal: 5,
          Plato: 2,
          Aristotle: 3,
          Seneca: 9,
          Sartre: 5,
          Crawford: 0
        }
      },
      2: {
        optionText: "Forming a band with my friends, spending years working towards semi-success",
        scores: {
          DFW: 7,
          Pascal: 5,
          Plato: 8,
          Aristotle: 8,
          Seneca: 1,
          Sartre: 5,
          Crawford: 10
        }
      }
    }
  },
  {
    id: 17,
    question: "Having a strong sense of justice is a burden, not a gift.",
    options: {
      1: {
        optionText: "True",
        scores: {
          DFW: 2,
          Pascal: 5,
          Plato: 2,
          Aristotle: 2,
          Seneca: 10,
          Sartre: 2,
          Crawford: 7
        }
      },
      2: {  
        optionText: "False"
        }
    }
  },
  {
    id: 18,
    question: "I can only live a happy life if my community is treated fairly, too.",
    options: {
      1: {
        optionText: "True",
        scores: {
          DFW: 8,
          Pascal: 1,
          Plato: 9,
          Aristotle: 9,
          Seneca: 1,
          Sartre: 0,
          Crawford: 4
        }
      },
      2: {  
        optionText: "False"
        }
    }
  },
  {
    id: 19,
    question: "I would rather...",
    options: {
      1: {
        optionText: "Work a 40 hour/week job doing community outreach earning 60k/yr",
        scores: {
          DFW: 8,
          Pascal: 8,
          Plato: 10,
          Aristotle: 7,
          Seneca: 0,
          Sartre: 5,
          Crawford: 10
        }
      },
      2: {
        optionText: "Work a 30 hour/week job as a day trader earning 100k/yr",
        scores: {
          DFW: 2,
          Pascal: 2,
          Plato: 0,
          Aristotle: 3,
          Seneca: 10,
          Sartre: 5,
          Crawford: 0
        }
      }
    }
  },
  {
    id: 20,
    question: "Work-life balance only matters if you don't like your job.",
    options: {
      1: {
        optionText: "True",
        scores: {
          DFW: 4,
          Pascal: 8,
          Plato: 2,
          Aristotle: 2,
          Seneca: 3,
          Sartre: 7,
          Crawford: 5
        }
      },
      2: {  
        optionText: "False"
        }
    }
  }
];
quizQuestions.forEach(question => {
  const secondOptionScores = Object.fromEntries(
    Object.entries(question.options[1].scores).map(([philosopher, score]) => [philosopher, 10 - score])
  ) as Record<string, number>;
  if(question.options[1].optionText === "True"){
    question.options[2].scores = secondOptionScores;
  }
  // Update the scores for the second option
});
//Frontend development is not fun!
const shuffleArray = (array: any[]) => {
    for (let i = array.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [array[i], array[j]] = [array[j], array[i]];
    }
  };

  // Shuffle the quizQuestions array
  shuffleArray(quizQuestions);
  let order = 1;
   // Reset order before the component is mounted
   onMounted(() => {
    order = 1;
  });
  const userResponses: UserResponses = Object.create(null);

 const philosophers: string[] = ["DFW", "Pascal", "Plato", "Aristotle", "Seneca", "Sartre", "Crawford"];
 const resultPhilosopher = ref<string | null>(null);
  // Define methods
  const updateUserResponse = (questionId: number, rating: number) => {
    if (!userResponses[questionId]) {
      userResponses[questionId] = {} as { rating: number };
    }
    userResponses[questionId] = rating;
  };

  const calculateResult = () => {
    console.log('calculating!')
    const scores: Record<string, number> = {}; // Accumulate scores for each philosopher

    for (const questionId in userResponses) {
      const response = userResponses[questionId];
      if (response) {

        const question = quizQuestions.find((q) => q.id === +questionId);
        if (question) {
          const option = question.options[response];
          if (option) {
            for (const philosopher in option.scores) {
              console.log(option.scores[philosopher])
              scores[philosopher] = (scores[philosopher] || 0) + option.scores[philosopher];
            }
          }
        }
      }
    }

    let maxScore = -1;
    let mostSimilarPhilosopher = "";
    console.log(scores)
    for (const philosopher in scores) {
      if (scores[philosopher] > maxScore) {
        maxScore = scores[philosopher];
        mostSimilarPhilosopher = philosopher;
      }
    }
    console.log(mostSimilarPhilosopher)
    resultPhilosopher.value = mostSimilarPhilosopher;
  };
</script>

  
<template>
  <div>
    <h1>Philosopher Quiz</h1>
    <div v-for="question in quizQuestions" :key="question.id">
      <h2>{{ order++ }}. {{ question.question }}</h2>
      <div v-for="(option, key) in question.options" :key="key">
        <label>
          <input
            type="radio"
            :name="'question_' + question.id"
            :value="key"
            v-model="userResponses[question.id]"
            @change="updateUserResponse(question.id, key)"
            :required="userResponses[question.id] === null"
          />
          {{ option.optionText }}
        </label>
      </div>
    </div>
    <button @click="calculateResult">Get Result</button>
    <div v-if="resultPhilosopher">
      <h1>Most Similar Philosopher: {{ resultPhilosopher }} <br> Thanks for taking the quiz!</h1>
    </div>
    <!-- TODO: Display result -->
  </div>
</template>
