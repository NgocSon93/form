<template>
  <form class="screen" @submit.prevent="onSubmit">
    <div class="container">
      <div class="row"><h1 class="title">Now, about your project...</h1></div>
      <div class="row">
        <div class="col-7">
          <div class="section">
            <p>
              We like being on a first-name basis, but it also helps us get in
              touch with you.
            </p>
            <div class="form-group">
              <div class="form-item col">
                <label for="name">What is your full name?</label>
                <input
                  id="name"
                  :class="{ error: error.status, success: success.status }"
                  type="text"
                  placeholder="John Smith"
                  v-model="quiz.fullname"
                />
                <p class="error-text" v-if="error.status">{{ error.text }}</p>
                <p class="success-text" v-if="success.status">
                  {{ success.text }}
                </p>
              </div>
              <div class="form-item col">
                <label for="email">What is your email address?</label>
                <input
                  id="email"
                  type="email"
                  placeholder="skyalbert.960@gmail.com"
                  v-model="quiz.email"
                />
                <p class="error-email" v-if="erroremail.status">
                  {{ erroremail.text }}
                </p>
                <p class="success-email" v-if="successemail.status">
                  {{ successemail.text }}
                </p>
              </div>
            </div>
          </div>
          <div class="section options">
            <p>
              What sort of creative work do you need help with? You can read
              about our services
            </p>
            <div class="row">
              <div class="col-4" v-for="option in jobOptions" :key="option.id">
                <div
                  class="block"
                  :style="{
                    backgroundColor: quiz.jobs.includes(option.id)
                      ? 'var(--primary)'
                      : '',
                  }"
                >
                  <label class="option">
                    <span>{{ option.name }}</span>
                    <input
                      type="checkbox"
                      :value="option.id"
                      v-model="quiz.jobs"
                    />
                    <span class="checkmark"></span>
                  </label>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="col-4">
          <div class="section right">
            <p>
              Tell us what you need help with, the purpose of this project and
              problems wr’re solving.
            </p>
            <div class="form-item">
              <label for="about">What is your project all about?</label>
              <textarea
                id="about"
                placeholder="Hey RHP Team, I’d love  to talk to you about  branding this Something AI  project we’re working..."
                v-model="quiz.desc"
              />
            </div>
            <div class="form-item">
              <ul class="items">
                <li class="item">
                  <div class="file">
                    <div class="file-icon">
                      <img src="../assets/images/file.png" alt="File Icon" />
                    </div>
                    <div class="file-name">
                      website-information-architecture.pdf
                    </div>
                    <div class="file-icon">
                      <img src="../assets/images/close.png" alt="Close Icon" />
                    </div>
                  </div>
                </li>
                <li class="item">
                  <div class="file">
                    <div class="file-icon">
                      <img src="../assets/images/file.png" alt="File Icon" />
                    </div>
                    <div class="file-name">logo-animation.mov</div>
                    <div class="file-icon">
                      <img src="../assets/images/close.png" alt="Close Icon" />
                    </div>
                  </div>
                </li>
                <li class="item">
                  <div class="file">
                    <div class="file-icon">
                      <img
                        src="../assets/images/upload.png"
                        alt="Upload Icon"
                      />
                    </div>
                    <div class="file-name">Attach files</div>
                  </div>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="action">
      <div class="container">
        <div class="remaining">3/6 questions remaining</div>
        <div class="progress">
          <div class="progress-inner">
            <div class="progress-mask"></div>
          </div>
        </div>
        <button type="submit" class="btn btn-submit">Submit</button>
      </div>
    </div>
  </form>
</template>
<script>
import { reactive } from "vue";
export default {
  setup() {
    const quiz = reactive({
      fullname: "",
      email: "",
      desc: "",
      jobs: [],
    });

    const error = reactive({
      text: "",
      status: false,
    });

    const erroremail = reactive({
      text: "",
      status: false,
    });
    const success = reactive({
      text: "",
      status: false,
    });
    const successemail = reactive({
      text: "",
      status: false,
    });

    const jobOptions = [
      { id: 1, name: "Branding" },
      { id: 2, name: "Strategy" },
      { id: 3, name: "Motion Design" },
      { id: 4, name: "Development" },
      { id: 5, name: "Product Design" },
      { id: 6, name: "Marketing" },
      { id: 7, name: "Copywriting" },
      { id: 8, name: "Advisory" },
      { id: 9, name: "Compositing" },
    ];

    const onSubmit = () => {
      console.log(quiz);
      if (quiz.fullname.length < 6 || quiz.fullname.length > 18) {
        error.text = "Look failed! Fullname should be 6-18 characters.";
        error.status = true;
        success.text = "";
        success.status = false;
      } else {
        error.text = "";
        error.status = false;
        success.text = "Look great!";
        success.status = true;
      }
      if (!quiz.email) {
        erroremail.text = "phai dien email bat buoc";
        erroremail.status = true;
        successemail.text = "";
        successemail.status = false;
      } else {
        erroremail.text = "";
        erroremail.status = false;
        successemail.text = "duoc roi day";
        successemail.status = true;
      }
    };

    return {
      quiz,
      error,
      success,
      jobOptions,
      onSubmit,
      successemail,
      erroremail,
    };
  },
};
</script>
