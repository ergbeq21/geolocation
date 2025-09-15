<script>
    let breitenGrad = '';
    let langenGrad = '';
    let genauigkeit = '';
    let watchId;

    function showLocation(position) {
        breitenGrad = position.coords.latitude;
        langenGrad = position.coords.longitude;
        genauigkeit = position.coords.accuracy;
    }

    function showError(error) {
        console.log("error", error);
    }

    function showPosition() {
        navigator.geolocation.getCurrentPosition(showLocation, showError);
    }

    function watchPosition() {
        watchId = navigator.geolocation.watchPosition(showLocation, showError, {
            enableHighAccuracy: true
        });
    }

    function removeLocation() {
        breitenGrad = '';
        langenGrad = '';
        genauigkeit = '';
        if (watchId) {
            navigator.geolocation.clearWatch(watchId);
            watchId = null;
        }
    }
</script>

<div class="flex flex-col items-center justify-center min-h-screen bg-gray-50 dark:bg-gray-900">
    <div class="flex flex-row items-center justify-center gap-2">
        <button
            onclick={showPosition}
            class="px-4 py-2 mb-6 bg-blue-600 hover:bg-blue-700 text-white font-semibold rounded-lg shadow-md transition"
        >
            Get Current Position
        </button>
        <button
            onclick={watchPosition}
            class="px-4 py-2 mb-6 bg-blue-600 hover:bg-blue-700 text-white font-semibold rounded-lg shadow-md transition"
        >
            Watch Position
        </button>
        <button
            onclick={removeLocation} 
            class="px-4 py-2 mb-6 bg-red-600 hover:bg-red-700 text-white font-semibold rounded-lg shadow-md transition"
        >
            Remove location
        </button>
    </div>

    <div class="w-full max-w-md bg-white dark:bg-gray-800 rounded-2xl shadow p-6">
        <h2 class="text-lg font-bold text-gray-800 dark:text-gray-200 mb-4">Your Location Data</h2>

        <div class="space-y-2 text-gray-700 dark:text-gray-300">
            <p><span class="font-semibold">Latitude:</span> {breitenGrad || "—"}</p>
            <p><span class="font-semibold">Longitude:</span> {langenGrad || "—"}</p>
            <p><span class="font-semibold">Accuracy:</span> {genauigkeit ?? `${genauigkeit} meters`}</p>
        </div>
    </div>
</div>
