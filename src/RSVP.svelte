<script>
  function handleOnSubmit(...args) {
    console.log(`args:`, args);
    const formData = new FormData(event.target);
    for (var pair of formData.entries()) {
      console.log(pair[0] + ": " + pair[1]);
    }
    if (document.getElementById("illbethere").checked) {
      //Yes radio button is checked
    }

    emailjs
      .send(
        process.env.service_id,
        process.env.template_id,
        { from_name: "fill this out", message: "fill this out" },
        process.env.emailjs_user_id
      )
      .then(
        (response) => {
          sending = false;
          addNotification({
            text: `You've been added to the mailing list!`,
            position: "top-center",
            type: "success",
          });
          console.log("SUCCESS!", response.status, response.text);
        },
        (err) => {
          addNotification({
            text: `That didn't work for some reason. Email me to make sure I get you on the list!`,
            position: "top-center",
            type: "warning",
          });
          sending = false;
          console.log("FAILED...", err);
        }
      );
  }
</script>

<div class="page">
  <div class="formHolder">
    <br />
    <br />
    <h1>RSVP</h1>
    <form on:submit|preventDefault={handleOnSubmit}>
      <h4>Can you make it</h4>
      <label class="radio-inline formfield">
        <input type="radio" id="illbethere" name="optradio" checked /> I'll be there!
      </label>
      <label class="radio-inline formfield">
        <input type="radio" name="optradio" /> Unfortunately I can't make it...
      </label>
      <h4>Your Name</h4>
      <input class="formfield" name="name" required />

      <h4>List Everyone You're RSVPing for (optional)</h4>
      <textarea class="formfield" name="additionalPeople" />

      <h4>Any Additional Info</h4>
      <textarea class="formfield" name="additionalInfo" />
      <br />
      <button type="submit"> Submit</button>
    </form>
  </div>
</div>

<style>
  .page {
    overflow-y: scroll;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
  }
  .formHolder {
    text-align: center;
    background-color: rgb(255 255 255 / 50%);
    z-index: 1;
    padding: 20px;
    max-width: 500px;
    align-self: center;
    justify-self: center;
  }

  .formfield {
    width: 300px;
    border-radius: 4px;
    margin-bottom: 10px;
    padding-left: 0.6em;
    padding-right: 0.6em;
    color: #363636;
  }

  button {
    width: 300px;
    border-radius: 4px;

    color: #ffffff;
    background-color: #dd9828;
    /* color: white; */
    outline: none;
    border: none;
    /* border-bottom: 1px solid #ffffff;
    border-left: 2px solid #ffffff; */
  }
  button:hover {
    background-color: #db8e12;
  }

  h1 {
    color: #3a3a3a;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

</style>
