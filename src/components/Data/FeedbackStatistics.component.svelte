<script>
    export let count = 0;
    export let averageRate = 0;

    averageRate = (averageRate == NaN) ? 0 : averageRate;
</script>

<div class="statistics">
    <h5>Reviews: <span>{count}</span></h5>
    <h5>Rating Average: <span>{averageRate}</span></h5>
</div>

<style>
	.statistics {
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
    .statistics h5 {
        font-weight: bold;
    }
</style>