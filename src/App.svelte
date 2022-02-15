<script>
  export let firstName = "";
  export let lastName = "";
  export let email = "";
  export let overThirteen = false;

  const validateSubmission = (v) => {
    console.log(v);
  };
</script>

<main>
  <h1>TNRIS Store Updates</h1>
  <p>
    We are building a store! We don't know for certain what our offerings will
    be, but we are doing research to find out what our users want. Subscribe to
    our mailing list below to get updates on our progress.
  </p>
  <form on:submit|preventDefault={validateSubmission}>
    <div class="inputsInline">
      <label for="firstName">
        First Name
        <input
          id="firstName"
          type="text"
          bind:value={firstName}
          minlength="3"
          maxlength="32"
          pattern="[a-zA-Z-]*"
          required
        />
      </label>

      <label for="lastName">
        Last Name
        <input
          id="lastName"
          type="text"
          bind:value={lastName}
          minlength="3"
          maxlength="32"
          pattern="[a-zA-Z-]*"
          required
        />
      </label>
    </div>
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
    <label for="overThirteen">
      <input type="checkbox" id="overThirteen" bind:checked={overThirteen} required pattern="true" />
      I am over the age of thirteen.
    </label>
    <button>Submit</button>
  </form>
</main>

<style lang="scss">
  main {
    padding: 1em;
    max-width: 100%;
    margin: 0 auto;
  }

  h1 {
    color: #38596d;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  form {
    padding: 16px;
    border: solid 1px lightgrey;
    border-radius: 8px;

    .inputsInline {
      display: inline-flex;
    }

    label {
      input,
      button {
        margin: 4px;
        margin-bottom: 8px;
        padding: 8px;
        display: block;
        border: solid 1px lightgray;

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
      max-width: none;
    }
  }
  @media (max-width: 639px) {
    form {
      .inputsInline {
        display: inline-block;
      }
    }
  }
</style>
