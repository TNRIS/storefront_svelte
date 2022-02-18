<script>
  export let email = "";
  export let overThirteen = false;

  const validateSubmission = (v) => {
    console.log(v);
  };
</script>

<main>
  <div id="left">
    <div id="interestStatement">
      <h1>TNRIS Store Updates</h1>
      <p>
        We are building a store! We don't know for certain what our offerings
        will be, but we are doing research to find out what our users want.
        Subscribe to our mailing list below to get updates on our progress.
      </p>
    </div>
    <form on:submit|preventDefault={validateSubmission}>
      <label for="email">
        Email
        <input
          id="email"
          type="email"
          bind:value={email}
          minlength="4"
          maxlength="64"
          required
        />
      </label>
      <button>Submit</button>
    </form>
  </div>
  <div id="right">
    <img id="image" src="#" alt="alternate_text" />
  </div>
</main>

<style lang="scss">
  main {
    padding: 1em;
    max-width: 100%;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(400px, 1fr));
    gap: 16px;

    #left,
    #right {
      border: solid 1px lightgrey;
      border-radius: 8px;
      padding: 16px;
    }

    #right {
      background: lightgray;
    }
  }

  h1 {
    color: #38596d;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  form {
    padding: 16px;

    label {
      input,
      button {
        margin: 4px;
        margin-bottom: 8px;
        padding: 8px;
        display: block;
        border: solid 1px lightgray;
      }

      input {
        &[type="checkbox"] {
          display: inline-block;
          padding: 8px;
        }
      }
    }

    input {
      &:invalid {
        border: 2px dashed red;
      }
      &:invalid:required {
        background: rgb(255, 216, 223);
      }
      &:valid {
        border: 2px solid black;
      }
    }
  }

  @media (min-width: 640px) {
    main {
      max-width: 1200px;
    }
  }
</style>
