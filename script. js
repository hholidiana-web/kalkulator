
let expression = "";

const result = document.getElementById("result");
const history = document.getElementById("history");

function append(value) {
    if (expression === "Error") {
        expression = "";
    }

    expression += value;
    result.value = expression;
}

function clearDisplay() {
    expression = "";
    result.value = "0";
    history.textContent = "";
}

function deleteLast() {
    expression = expression.slice(0, -1);
    result.value = expression || "0";
}

function calculate() {
    try {
        if (!expression) return;

        // Hanya izinkan karakter matematika
        if (!/^[0-9+\-*/%.() ]+$/.test(expression)) {
            throw new Error("Input tidak valid");
        }

        let calculation = expression;

        // Persen sederhana: 50% menjadi 50/100
        calculation = calculation.replace(
            /(\d+(?:\.\d+)?)%/g,
            "($1/100)"
        );

        const answer = Function(
            '"use strict"; return (' + calculation + ')'
        )();

        if (!Number.isFinite(answer)) {
            throw new Error("Hasil tidak valid");
        }

        history.textContent = expression + " =";

        expression = String(
            Number(answer.toPrecision(12))
        );

        result.value = expression;

    } catch (error) {
        result.value = "Error";
        expression = "";
    }
}

function toggleTheme() {
    document.body.classList.toggle("light");
}

// Dukungan keyboard
document.addEventListener("keydown", function(event) {
    if ("0123456789+-*/.%()".includes(event.key)) {
        append(event.key);
    }

    if (event.key === "Enter") {
        calculate();
    }

    if (event.key === "Backspace") {
        deleteLast();
    }

    if (event.key === "Escape") {
        clearDisplay();
    }
});
