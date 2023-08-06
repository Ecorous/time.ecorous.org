<script lang="ts">
    let date: any;
    let time: any;
    let unixTime: any;
    // Get the user's timezone offset in minutes
    var userTimezoneOffset = new Date().getTimezoneOffset();

    // Convert the offset to milliseconds
    userTimezoneOffset *= 60 * 1000;

    // Get the current time in UTC
    var currentUTCTime = new Date().getTime();

    // Calculate the time in the user's timezone
    var currentTimeInUserTimezone = new Date(
        currentUTCTime + userTimezoneOffset
    );

    // Format the date in the user's timezone as yyyy-mm-dd
    date = currentTimeInUserTimezone.toISOString().slice(0, 10);

    // Adjust the time to the user's timezone and round down
    var hours = Math.floor(
        (currentTimeInUserTimezone.getHours() * 60 +
            currentTimeInUserTimezone.getMinutes() -
            userTimezoneOffset / (60 * 1000)) /
            60
    );
    var minutes = currentTimeInUserTimezone.getMinutes();
    time =
        hours.toString().padStart(2, "0") +
        ":" +
        minutes.toString().padStart(2, "0");

    // Display the date and time
    console.log("Date in user timezone: " + date);
    console.log("Time in user timezone (rounded down): " + time);

    function triggerUpdate(element: String) {
        let datetime = `${date} ${time}`
        if (element == "date") {
            console.log(date)
        } else if (element == "time") {
            console.log(time)
        } else {
            console.log(datetime)
        }

        let dateTime = new Date(datetime)
        unixTime = dateTime.getTime() / 1000
    }
</script>

<h1>funny time thing</h1>
<p>this site is made by ecorous</p>
<p>it was very crappily made</p>
<p>have fun!</p>

<label for="date-time-input">Select a date and time:</label>
<input
    bind:value={date}
    on:change={() => triggerUpdate("date")}
    type="date"
    id="date-time-input"
    name="date"
/>
<input
    bind:value={time}
    on:change={() => triggerUpdate("time")}
    type="time"
    id="date-time-input"
    name="time"
/>

<p>Unix Time is: {unixTime}</p>

<button on:click={() => triggerUpdate("button")}>Update</button>

<style>
    @import url("https://unpkg.com/@catppuccin/palette/css/catppuccin.css");
    @import url("https://fonts.googleapis.com/css2?family=Martian Mono&display=swap");

    :root {
        font-family: "Martian Mono";
        background-color: var(--ctp-mocha-base);
        color: var(--ctp-mocha-text);
    }

    input {
        background-color: var(--ctp-mocha-crust);
        border-color: transparent;
        color: var(--ctp-mocha-text);
        padding: 5px;
        border-radius: 10px;
    }
</style>
