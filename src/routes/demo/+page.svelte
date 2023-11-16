<script>
  import { base } from '$app/paths';
  import IconResponse from "../../lib/component/patient/IconResponse.svelte";
  import VisResponse from "../../lib/component/doctor/VisResponse.svelte";
  import MyTitle from "../../lib/component/MyTitle.svelte";

  let buttonStatus = "Start";

  let patient_circle_text = "Hi there!";
  let patient_initial_prompt = "Don't worry, things will be OK";

  let doctor_circle_text = "Hi there!";
  let doctor_initial_prompt = "I will assist you in the entire process";


  let patient_status = "inactive";
  let doctor_status = "inactive";

  let image_url;
  let showText = true;

  const handleClick = async () => {
    
    const originalStatus = buttonStatus;

    if (originalStatus === "Start" || originalStatus === "Continue" || originalStatus === "Next") {
      buttonStatus = "Running...";

      if (originalStatus === "Start") {
        await welcome();
        buttonStatus = "Continue";
      } else if (originalStatus === "Continue") {
        await scnario_1();
        buttonStatus = "Next";
      } else if (originalStatus === "Next") {
        await scnario_2();
        buttonStatus = "Finish";
      }
    }
  }

  // Welcome
  async function welcome() {

    return new Promise((resolve, reject) => {
      // patient
      let audio = new Audio("/patient/Turn to the patient and temperature and.mp3");
      patient_status = "active";
      patient_initial_prompt = "请您放心，这次的放疗会比以前更加轻松。我们使用了新的技术，能够更精准地定位，减少对周围健康组织的影响，因此您可能感觉不到那么多不适。";
      audio.play();
      patient_circle_text = "🐱";


      // doctor
      audio.onended = function() {
        setTimeout(() => {
          patient_status = "inactive";
          let doctorAudio = new Audio("/doctor/Check medical instruments.mp3");
          doctor_status = "active";
          doctorAudio.play();
          image_url = "/welcome.jpg";
          showText = false
          doctor_initial_prompt = "医生，患者的心率为75次/分钟，血压为120/80毫米汞柱，呼吸频率稳定在每分钟18次。辐射吸收剂量控制在安全范围内，未超过预定的最大值。我们可以开始放疗了。"
          doctorAudio.onended = function() {
            doctor_status = "inactive";
            resolve();
          };
        }, 1000);
      };
    })  
  };

  async function scnario_1() {

    return new Promise((resolve, reject) => {

      showText = true;
      doctor_initial_prompt = "I will assist you in the entire process";

      console.log("hjhhh")
      // patient   
      let audio = new Audio("/patient/scenario_1.mp3");
      patient_status = "active";
      patient_initial_prompt = "您感觉怎么样？请告诉我如果您感到不舒服";
      audio.play();
      patient_circle_text = "🤗";


      // doctor
      audio.onended = function() {
        setTimeout(() => {
          patient_status = "inactive";
          let doctorAudio = new Audio("/doctor/scenario_1.mp3");
          doctor_status = "active";
          image_url = "/scnario_1.jpg";
          showText = false
          doctorAudio.play();
          doctor_circle_text = "👍";
          doctor_initial_prompt = "医生，患者的生命体征依然稳定，但他看起来面色苍白，可能表明痛苦或不适。心率上升到了82次每分钟，血压稍微升高到了125/85毫米汞柱。我会关注患者的呼吸模式，以确定是否有呼吸困难的迹象，来考虑减少辐射剂量。你觉得可以吗？";
          doctorAudio.onended = function() {
            doctor_status = "inactive";
            resolve();
          };
        }, 1000);
      };
    })

  };

  async function scnario_2() {

    return new Promise((resolve, reject) => {

      showText = true;
      doctor_initial_prompt = "I will assist you in the entire process";

      patient_circle_text = "Hi there!";
      patient_initial_prompt = "Don't worry, things will be OK";

      // doctor   
      let audio = new Audio("/doctor/scenario_2.mp3");
      doctor_status = "active";
      doctor_initial_prompt = "医生，放疗整体上非常成功。患者体征稳定，但观察到轻微的皮肤反应，可能是对辐射的敏感反应。我建议进行皮肤护理，并密切监控患者的恢复情况。我们可以提供抗炎或镇痒药膏以减轻不适，并建议患者保持良好的生活习惯，以促进皮肤的自然愈合。";
      audio.play();
      doctor_circle_text = "🤗";


      // patient
      audio.onended = function() {
        setTimeout(() => {
          patient_status = "inactive";
          let patientAudio = new Audio("/patient/scnarios_2.mp3");
          patient_status = "active";
          patientAudio.play();
          patient_circle_text = "👍";
          patient_initial_prompt = "嗨！放疗整体非常成功，但您的皮肤出现轻微反应。因此，建议您多休息以助恢复，多喝水以排除体内毒素，避免剧烈运动减少皮肤摩擦。医生为您开具了抗炎或镇痒药膏，加速康复。";
          patientAudio.onended = function() {
            patient_status = "inactive";
            resolve();
          };
        }, 1000);
      };
    })
  };

</script>


<div class="top-wrapper">
  <div class="patient-doctor-wrapper">
    <div class="patient-wrapper">
      <div class="title">
        <MyTitle title="Patient" status={patient_status}/>
      </div>
      <div class="content">
        <IconResponse circle_text={patient_circle_text} initial_prompt={patient_initial_prompt}/>
      </div>
    </div>
  
    <div class="doctor-wrapper">
      <div class="title">
        <MyTitle title="Doctor" status={doctor_status} />
      </div>
      <div class="content">
        <VisResponse vis_text={doctor_circle_text} initial_prompt={doctor_initial_prompt} 
          image_url={image_url} isText={showText}
        />
      </div>
    </div>
  </div>
  <div class="button-wrapper">
    <button class={buttonStatus == "Start" ? "green-stasrt" : "green-running"} on:click={handleClick}>{buttonStatus}</button>
  </div>
</div>



<style>

  :global(body) {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh; 
        margin: 0;
        background: #F9F3EB;
    }

  button.green-stasrt {
    display: flex;
    width: 100px;
    padding: 8px 12px;
    justify-content: center;
    align-items: center;
    gap: 10px;
    border: none;

    border-radius: 4px;
    background: #0D3C26;

    color: rgb(225, 237, 231);
    font-family: Inter;
    font-size: 24px;
    font-weight: 600;
    line-height: 100%; /* 30px */
  }

  button.green-stasrt {
    box-shadow: 0px 0px 8px rgba(50, 46, 42, 0.10);
    cursor: pointer;
  }

  button.green-running {
    display: flex;
    width: 150px;
    padding: 8px 12px;
    justify-content: center;
    align-items: center;
    gap: 10px;
    border: none;

    border-radius: 4px;
    background: #052013;

    color: rgb(225, 237, 231);
    font-family: Inter;
    font-size: 24px;
    font-weight: 600;
    line-height: 100%; /* 30px */
  }

  div.top-wrapper {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 20vh;
  }

  div.patient-doctor-wrapper {
    display: flex;
    width: 95vw;
    justify-content: center;
    align-items: flex-start;
    gap: 80px;
  }

  div.patient-wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20vh;
    flex: 1 0 0;
    align-self: stretch;
  } 

  div.doctor-wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20vh;
    flex: 1 0 0;
    align-self: stretch;
  }

  div.title {
    display: flex;
    align-items: center;
    align-self: stretch;
    border-bottom: 1.2px solid #0D3C26;
  }
</style>