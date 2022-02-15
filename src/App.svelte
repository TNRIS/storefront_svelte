<script>
  export let firstName = "";
  export let lastName = "";
  export let email = "";
  export let overThirteen = false;
</script>

<main>
  <h1>TNRIS Store Updates</h1>
  <p>
    We are building a store! We don't know for certain what our offerings will
    be, but we are doing research to find out what our users want. Subscribe to
    our mailing list below to get updates on our progress.
  </p>
  <form>
    <div class="inputsInline">
      <label for="firstName">
        First Name
        <input id="firstName" bind:value={firstName} />
      </label>

      <label for="lastName">
        Last Name
        <input id="lastName" bind:value={lastName} />
      </label>
    </div>
    <label for="email">
      Email
      <input id="email" bind:value={email} />
    </label>
    <label for="overThirteen">
      <input type="checkbox" id="overThirteen" bind:value={overThirteen} />
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
      input, button {
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
