<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Genotype Inheritance Simulator</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; line-height: 1.6; color: #333; max-width: 800px; margin: 0 auto; padding: 20px; background-color: #f4f7f6; }
        .container { background: white; padding: 30px; border-radius: 12px; box-shadow: 0 4px 6px rgba(0,0,0,0.1); }
        h1 { color: #2c3e50; text-align: center; }
        .status-box { background: #e8f4f8; border-left: 5px solid #3498db; padding: 15px; margin: 20px 0; }
        .controls { display: flex; justify-content: center; gap: 10px; margin-bottom: 20px; }
        button { padding: 10px 20px; font-size: 16px; cursor: pointer; border: none; border-radius: 5px; transition: 0.3s; }
        .btn-primary { background-color: #3498db; color: white; }
        .btn-primary:hover { background-color: #2980b9; }
        .btn-reset { background-color: #e74c3c; color: white; }
        table { width: 100%; border-collapse: collapse; margin-top: 20px; }
        th, td { border: 1px solid #ddd; padding: 12px; text-align: center; }
        th { background-color: #34495e; color: white; }
        tr:nth-child(even) { background-color: #f9f9f9; }
        .highlight { font-weight: bold; color: #e67e22; }
    </style>
</head>
<body>

<div class="container">
    <h1>Genotype Determination Sim</h1>
    
    <div class="status-box" id="status">
        <strong>Current Status:</strong> Trial 1, Generation 0. Starting Genotype: <span class="highlight">Ll</span>
    </div>

    <div class="controls">
        <button class="btn-primary" onclick="nextGeneration()" id="nextBtn">Simulate Generation</button>
        <button class="btn-reset" onclick="resetSimulation()">Reset All Trials</button>
    </div>

    <table id="resultsTable">
        <thead>
            <tr>
                <th>Generation</th>
                <th>Trial 1 Genotype</th>
                <th>Trial 2 Genotype</th>
                <th>Trial 3 Genotype</th>
            </tr>
        </thead>
        <tbody>
            <tr><td>Start</td><td>Ll</td><td>Ll</td><td>Ll</td></tr>
            <tr><td>Gen 1</td><td id="t1-g1">-</td><td id="t2-g1">-</td><td id="t3-g1">-</td></tr>
            <tr><td>Gen 2</td><td id="t1-g2">-</td><td id="t2-g2">-</td><td id="t3-g2">-</td></tr>
            <tr><td>Gen 3</td><td id="t1-g3">-</td><td id="t2-g3">-</td><td id="t3-g3">-</td></tr>
            <tr><td>Gen 4</td><td id="t1-g4">-</td><td id="t2-g4">-</td><td id="t3-g4">-</td></tr>
            <tr><td>Gen 5</td><td id="t1-g5">-</td><td id="t2-g5">-</td><td id="t3-g5">-</td></tr>
        </tbody>
    </table>
</div>

<script>
    let currentTrial = 1;
    let currentGen = 1;
    let currentGenotype = "Ll";

    function getGametes(genotype) {
        if (genotype === "LL") return ['L', 'L', 'L', 'L'];
        if (genotype === "ll") return ['l', 'l', 'l', 'l'];
        return ['L', 'L', 'l', 'l']; // For Ll
    }

    function simulateMating(myGenotype) {
        // Step A & E: Get my gametes based on current genotype
        let myCards = getGametes(myGenotype);
        
        // Step B: Simulate a random partner's genotype 
        // In a real classroom this is a person; here we assume a random distribution (Hardy-Weinberg start)
        let partnerGenotypes = ["LL", "Ll", "ll"];
        let partnerGenotype = partnerGenotypes[Math.floor(Math.random() * partnerGenotypes.length)];
        let partnerCards = getGametes(partnerGenotype);

        // Step C: Draw one card from each (The "Meiosis/Fertilization" shuffle)
        let myAllele = myCards[Math.floor(Math.random() * 4)];
        let partnerAllele = partnerCards[Math.floor(Math.random() * 4)];

        // Combine and sort (so 'lL' becomes 'Ll')
        let newGenotype = [myAllele, partnerAllele].sort().join("");
        return newGenotype;
    }

    function nextGeneration() {
        if (currentTrial > 3) return;

        let result = simulateMating(currentGenotype);
        document.getElementById(`t${currentTrial}-g${currentGen}`).innerText = result;
        currentGenotype = result;

        currentGen++;

        if (currentGen > 5) {
            if (currentTrial < 3) {
                alert(`Trial ${currentTrial} complete! Moving to Trial ${currentTrial + 1}. Starting back at Ll.`);
                currentTrial++;
                currentGen = 1;
                currentGenotype = "Ll";
            } else {
                document.getElementById("nextBtn").disabled = true;
                alert("All trials complete!");
            }
        }
        updateStatus();
    }

    function updateStatus() {
        const status = document.getElementById("status");
        if (currentTrial <= 3) {
            status.innerHTML = `<strong>Current Status:</strong> Trial ${currentTrial}, Generation ${currentGen-1} complete. Current Genotype: <span class="highlight">${currentGenotype}</span>`;
        } else {
            status.innerHTML = "<strong>Simulation Finished.</strong>";
        }
    }

    function resetSimulation() {
        location.reload();
    }
</script>

</body>
</html>
