<script>
  export let email = undefined;

  export let submitResp = undefined;

  const submitSubscription = async (data) => {
    const campaignId = "de4b945e-b682-46e2-9e1b-0d6fe1854a13";
    data["campaign"] = campaignId;

    let form_data = new FormData();

    for (var key in data) {
      form_data.append(key, data[key]);
    }

    const resp = await fetch(
      "https://api.tnris.org/api/v1/contact/campaignsubscription",
      {
        method: "POST",
        body: form_data,
      }
    );

    if (resp.ok) {
      const okResp = await resp.json();
      submitResp = { status: resp.status, data: okResp };
      console.log(submitResp);
      email = undefined;
      return submitResp;
    } else {
      const errJson = await resp.json();
      submitResp = { status: resp.status, data: errJson };
      console.log(submitResp);
      email = undefined;
      return submitResp;
    }
  };

  function validateEmail(email) {
    var re = /\S+@\S+\.\S+/;
    return re.test(email);
  }

  const onSubmit = (e) => {
    const formData = new FormData(e.target);
    const data = {};
    for (let field of formData) {
      const [key, value] = field;
      data[key] = value;
    }
    if (data["email"] && validateEmail(data["email"])) {
      submitSubscription(data);
    } else {
      console.log("email not set or invalid");
    }
  };
</script>

<main>
  <section id="contentWrapper">
    <div id="contentContainer">
      <div id="interestStatement">
        <h1>Map Products Supporting Texas' GIS Community</h1>
        <p>
          We're excited to be developing a new store concept of curated
          historical, artistic, and GIS branded products with profits
          benefitting the Texas GIS Forum and education initiatives.
        </p>
        <p>
          <strong>
            Sign up below to be updated on our progress and launch!
          </strong>
        </p>
      </div>
      <form on:submit|preventDefault={onSubmit}>
        <input
          placeholder="enter your email"
          id="email"
          type="email"
          name="email"
          bind:value={email}
          minlength="4"
          maxlength="64"
          required
        />
        {#if submitResp}
          <div id="submissionResponse">
            {#if submitResp.status == 400}
              <p class="errorResponse">{submitResp.data.email[0]}</p>
            {/if}
            {#if submitResp.status == 201}
              <p class="successResponse">
                Thanks for signing up and showing interest in the store! We'll
                let you know about progress and launch updates.
              </p>
            {/if}
          </div>
        {/if}
        <button id="submitEmail" class="primary">Submit</button>
      </form>
    </div>
  </section>
  <img
    id="mobileImage"
    src="build/images/TNRIS_StoreLandingImage_220222.png"
    alt="TNRIS concept art displayed on showcase wall"
  />
</main>
<footer>
  <section id="footerContent">
    <a href="https://tnris.org/site-policies/#privacy-and-security-policy"
      >Privacy/Security Policy</a
    >
    <div>
      <span>
        Content of this site © Texas Natural Resources Information System and
        Texas Water Development Board unless otherwise noted.
      </span>
    </div>
  </section>
</footer>

<style lang="scss">
  img#mobileImage {
    max-width: 100%;
    margin-top: 32px;
  }
  form {
    display: grid;
    grid-template-rows: auto;
  }
  .successResponse {
    color: green;
    font-weight: 500;
    font-size: 18px;
    line-height: 24px;
  }
  .errorResponse {
    color: red;
    font-weight: 500;
    font-size: 18px;
    line-height: 24px;
  }
  @media (min-width: 640px) {
    main {
      margin: auto;
      width: 100vw;
      height: 100%;
    }
    section#contentWrapper {
      padding: 24px;
      padding-top: 72px;
      max-width: 1400px;
      margin: 0 auto;

      #contentContainer {
        padding: 25px;
        border-radius: 8px;
        background: #ffffff;
        max-width: 550px;
      }
    }
    img#mobileImage {
      display: none;
    }
    :global(html) {
      main {
        background: url("images/TNRIS_StoreLandingImage_220222.png");
        background-repeat: no-repeat;
        background-position: bottom;
        background-size: cover;
      }
    }
  }
  :global(html) {
    margin: 0;
    padding: 0;

    h1 {
      font-family: Lora;
      font-style: normal;
      font-weight: 400;
      font-size: 55px;
      line-height: 70px;
      margin-top: 0px;
    }
    p {
      font-family: Quicksand;
      font-style: normal;
      font-weight: 500;
      font-size: 24px;
      line-height: 30px;
    }
    footer {
      max-width: 100%;
      background: #ffffff;
      bottom: 0;
      padding: 20px;

      a {
        font-size: 18px;
        font-weight: 500;
        text-decoration: underline;
      }
      span {
        font-size: 18px;
      }

      #footerContent {
        max-width: 1400px;
        display: grid;
        grid-template-columns: auto auto;
        gap: 16px;
        margin: auto;
      }
    }
    form {
      input {
        background: #ffffff;
        border: 1px solid #000000;
        box-sizing: border-box;
        border-radius: 8px;
        padding: 12px 20px;

        &:invalid {
          border: 2px dashed rgb(219, 113, 113);
        }
        &:valid {
          border: 2px solid black;
        }
        &:blank,
        &:default {
          border: 1px solid #000000;
          box-sizing: border-box;
          border-radius: 8px;
        }
      }
      button {
        border-radius: 8px;
        text-transform: uppercase;
        padding: 14px 20px;

        &.primary {
          background: #000000;
          color: #ffffff;
          font-weight: 700;
        }
      }
    }

    @media (max-width: 640px) {
      main {
        padding: 14px;
      }
      footer {
        text-align: center;
        #footerContent {
          display: grid;
          grid-template-columns: auto;
        }
      }
      p {
        font-size: 14px;
        line-height: 17px;
      }
      h1 {
        font-size: 36px;
        line-height: 46px;
      }
    }
  }
</style>
