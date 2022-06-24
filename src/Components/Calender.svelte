
<script>
    
	const date = new Date();

	const today = {
		dayNumber : date.getDate(),
		month : date.getMonth(),
		year : date.getFullYear()
	}

	const monthNames = ["January", "Febuary", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];

	let monthIndex = date.getMonth();
	$: month = monthNames[monthIndex];
	let year = date.getFullYear();

	$: getFirstDayIndex = new Date(year, monthIndex, 1).getDay();
	$: numberOfDays = new Date(year, monthIndex + 1, 0 ).getDate();
	
	$: calenderCellQty = getFirstDayIndex <= 4 ? 35 : 42;
	// let today = date.getDate();

	const goToPrevMonth = () => {
		if(monthIndex <= 0){
			year -= 1;
			return monthIndex = 11;
		}
		monthIndex -= 1;
	}

	const goToNextMonth = () => {
		if(monthIndex >= 11){
			year += 1;
			return monthIndex = 0;
		}
		monthIndex += 1;
	}

    const goToNextYear = () => { 
        year += 1;
    }

    const goToPrevYear = () => {
        year -= 1;
    }

	$: console.log(`Month : ${monthIndex} First Day Index : ${getFirstDayIndex} Last Day : ${numberOfDays}` )
</script>

<main>
    
<div class="month">
    <div class="year">
        <ul>
            <li class="next-year" on:click={goToNextYear}>&#10095;</li>
            <li class="prev-year" on:click={goToPrevYear}>&#10094;</li>
        </ul>
    </div>
	<ul>
	  <li class="prev" on:click={goToPrevMonth}>&#10094;</li>
	  <li class="next" on:click={goToNextMonth}>&#10095;</li>
      

	  <li>{month}<br>
		<span style="font-size:18px">{year}</span>
	</li>
	</ul>
 </div>
  
  <ul class="weekdays">
	<li>Sun</li>
	<li>Mon</li>
	<li>Tue</li>
	<li>Wed</li>
	<li>Thu</li>
	<li>Fri</li>
	<li>Sat</li>
	
  </ul>
  
  <ul class="days">
	{#each Array(calenderCellQty) as _, i }
	    {#if i< getFirstDayIndex || i >= numberOfDays + getFirstDayIndex}
	    	<li>&nbsp;</li>
	    {:else}
	        <li on:click class:active = {i === today.dayNumber + (getFirstDayIndex - 1) && 
	    			monthIndex === today.month && year === today.year}>{(i - getFirstDayIndex) + 1}</li>
	    {/if}
	{/each}
		
  </ul>

  <div class="month">
    <div class="year">
        <ul>
            <!-- <li class="next-year" on:click={goToNextYear}>&#10095;</li>
            <li class="prev-year" on:click={goToPrevYear}>&#10094;</li> -->
        </ul>
    </div>
	<ul>
	  <!-- <li class="prev" on:click={goToPrevMonth}>&#10094;</li>
	  <li class="next" on:click={goToNextMonth}>&#10095;</li>
       -->

	  <li>{monthNames[monthIndex + 1]}<br>
		<span style="font-size:18px">{year}</span>
	</li>
	</ul>
 </div>
  
  <ul class="weekdays">
	<li>Sun</li>
	<li>Mon</li>
	<li>Tue</li>
	<li>Wed</li>
	<li>Thu</li>
	<li>Fri</li>
	<li>Sat</li>
	
  </ul>
  
  <ul class="days">
	{#each Array(calenderCellQty) as _, i }
	{#if i< getFirstDayIndex || i >= numberOfDays + getFirstDayIndex}
		<li>&nbsp;</li>
	{:else}
	<li on:click class:active = {i === today.dayNumber + (getFirstDayIndex - 1) && 
				monthIndex + 1 === today.month && year === today.year}>{(i - getFirstDayIndex) + 1}</li>
	{/if}
	{/each}
		
  </ul>

  <div class="month">
    <div class="year">
        <ul>
            <!-- <li class="next-year" on:click={goToNextYear}>&#10095;</li>
            <li class="prev-year" on:click={goToPrevYear}>&#10094;</li> -->
        </ul>
    </div>
	<ul>
	  <!-- <li class="prev" on:click={goToPrevMonth}>&#10094;</li>
	  <li class="next" on:click={goToNextMonth}>&#10095;</li>
       -->

	  <li>{monthNames[monthIndex + 2]}<br>
		<span style="font-size:18px">{year}</span>
	</li>
	</ul>
 </div>
  
  <ul class="weekdays">
	<li>Sun</li>
	<li>Mon</li>
	<li>Tue</li>
	<li>Wed</li>
	<li>Thu</li>
	<li>Fri</li>
	<li>Sat</li>
	
  </ul>
  
  <ul class="days">
	{#each Array(calenderCellQty) as _, i }
	{#if i< getFirstDayIndex || i >= numberOfDays + getFirstDayIndex}
		<li>&nbsp;</li>
	{:else}
	<li on:click class:active = {i === today.dayNumber + (getFirstDayIndex - 1) && 
				monthIndex + 2 === today.month && year === today.year}>{(i - getFirstDayIndex) + 1}</li>
	{/if}
	{/each}
		
  </ul>

</main>

<style>

ul {list-style-type: none;}
main {font-family: Verdana, sans-serif;}

/* Month header */
.month {
  padding: 70px 25px;
  width: auto;
  background: #ff670f;
  text-align: center;
}

/* Month list */
.month ul {
  margin: 0;
  padding: 0;
}

.month ul li {
  color: white;
  font-size: 20px;
  text-transform: uppercase;
  letter-spacing: 3px;
}

/* Previous button inside month header */
.month .prev {
  float: left;
  padding-top: 10px;
  cursor: pointer;
}

/* Next button */
.month .next {
  float: right;
  padding-top: 10px;
  cursor: pointer;
}

.year .next-year{
    float: right;
  padding-top: 10px;
  cursor: pointer;
}

.year .prev-year{
    float: left;
  padding-top: 10px;
  cursor: pointer;
}

/* Weekdays (Mon-Sun) */
.weekdays {
  margin: 0;
  padding: 10px 0;
  background-color:#ddd;
}

.weekdays li {
  display: inline-block;
  width: 13.6%;
  color: rgb(0, 0, 0);
  text-align: center;
}

/* Days (1-31) */
.days {
  padding: 10px 0;
  background: #eee;
  margin: 0;
}

.days li {
  list-style-type: none;
  display: inline-block;
  width: 11.6%;
  text-align: center;
  /* margin-bottom: 1px; */
  font-size:  1.2em;;
  color: rgb(0, 0, 0);
  cursor: pointer;
  padding: 9px;
  border: 1px solid black;
}

/* Highlight the "current" day */
.active {
  padding: 5px;
  background:  #ff670f;
  color: white !important
}

</style>