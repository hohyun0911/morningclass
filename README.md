# morningclass
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>16인 본1부3</title>
    <style>
        .container {
            max-width: 1000px;
            margin: 0 auto;
            font-family: Arial, sans-serif;
        }
        .row-group {
            display: flex;
            justify-content: space-between;
        }
        .column {
            display: flex;
            flex-direction: column;
            width: 48%;
            position: relative;
        }
        .row {
            display: flex;
            align-items: center;
            margin-bottom: 10px;
        }
        .row label {
            flex: 1;
            margin-right: 5px;
        }
        .row input[type="number"] {
            width: 50px;
            margin-right: 1px;
        }
        #remainingSum {
            font-weight: bold;
            margin-bottom: 10px;
        }
        .divider {
            border-top: 1px solid #000;
            margin: 10px 0;
        }
        .center-divider {
            position: absolute;
            top: 0;
            bottom: 0;
            right: -10px;
            width: 1px;
            background-color: #000;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>16인 본1부3 폿본 체크</h1>
        <div class="row-group">
            <!-- Left Column: 1-1 to 1-4, 3-1 to 3-4 -->
            <div class="column" id="leftSection">
                <div class="row">
                    <label for="input1-1">1-1:</label>
                    <input type="checkbox" id="checkbox1-1">
                    <input type="number" id="input1-1" min="0" max="4" value="0">
                </div>
                <div class="row">
                    <label for="input1-2">1-2:</label>
                    <input type="checkbox" id="checkbox1-2">
                    <input type="number" id="input1-2" min="0" max="4" value="0">
                </div>
                <div class="row">
                    <label for="input1-3">1-3:</label>
                    <input type="checkbox" id="checkbox1-3">
                    <input type="number" id="input1-3" min="0" max="4" value="0">
                </div>
                <div class="row">
                    <label for="input1-4">1-4:</label>
                    <input type="checkbox" id="checkbox1-4">
                    <input type="number" id="input1-4" min="0" max="4" value="0">
                </div>
                <div class="divider"></div>
                <div class="row">
                    <label for="input3-1">3-1:</label>
                    <input type="checkbox" id="checkbox3-1">
                    <input type="number" id="input3-1" min="0" max="4" value="0">
                </div>
                <div class="row">
                    <label for="input3-2">3-2:</label>
                    <input type="checkbox" id="checkbox3-2">
                    <input type="number" id="input3-2" min="0" max="4" value="0">
                </div>
                <div class="row">
                    <label for="input3-3">3-3:</label>
                    <input type="checkbox" id="checkbox3-3">
                    <input type="number" id="input3-3" min="0" max="4" value="0">
                </div>
                <div class="row">
                    <label for="input3-4">3-4:</label>
                    <input type="checkbox" id="checkbox3-4">
                    <input type="number" id="input3-4" min="0" max="4" value="0">
                </div>
                <div class="center-divider"></div>
            </div>

            <!-- Right Column: 2-1 to 2-4, 4-1 to 4-4 -->
            <div class="column" id="rightSection">
                <div class="row">
                    <label for="input2-1">2-1:</label>
                    <input type="checkbox" id="checkbox2-1">
                    <input type="number" id="input2-1" min="0" max="4" value="0">
                </div>
                <div class="row">
                    <label for="input2-2">2-2:</label>
                    <input type="checkbox" id="checkbox2-2">
                    <input type="number" id="input2-2" min="0" max="4" value="0">
                </div>
                <div class="row">
                    <label for="input2-3">2-3:</label>
                    <input type="checkbox" id="checkbox2-3">
                    <input type="number" id="input2-3" min="0" max="4" value="0">
                </div>
                <div class="row">
                    <label for="input2-4">2-4:</label>
                    <input type="checkbox" id="checkbox2-4">
                    <input type="number" id="input2-4" min="0" max="4" value="0">
                </div>
                <div class="divider"></div>
                <div class="row">
                    <label for="input4-1">4-1:</label>
                    <input type="checkbox" id="checkbox4-1">
                    <input type="number" id="input4-1" min="0" max="4" value="0">
                </div>
                <div class="row">
                    <label for="input4-2">4-2:</label>
                    <input type="checkbox" id="checkbox4-2">
                    <input type="number" id="input4-2" min="0" max="4" value="0">
                </div>
                <div class="row">
                    <label for="input4-3">4-3:</label>
                    <input type="checkbox" id="checkbox4-3">
                    <input type="number" id="input4-3" min="0" max="4" value="0">
                </div>
                <div class="row">
                    <label for="input4-4">4-4:</label>
                    <input type="checkbox" id="checkbox4-4">
                    <input type="number" id="input4-4" min="0" max="4" value="0">
                </div>
            </div>
        </div>

        <p id="remainingSum">남은 합: 16</p>
        <button id="generateButton" disabled>계산</button>
        <button id="resetButton">초기화</button>

        <h2>결과:</h2>
        <div id="resultSection">
            <p></p>
        </div>
    </div>
    <script>
        const generateButton = document.getElementById('generateButton');
        const resetButton = document.getElementById('resetButton');
        const inputElements = document.querySelectorAll('input[type="number"]');
        const checkboxElements = document.querySelectorAll('input[type="checkbox"]');
        const remainingSumElement = document.getElementById('remainingSum');
        const resultSection = document.getElementById('resultSection');
    
        // Update remaining sum and enable/disable button
        function updateRemainingSum() {
            const total = Array.from(inputElements).reduce((sum, input) => sum + (parseInt(input.value) || 0), 0);
            const remaining = 16 - total;
    
            if (remaining > 0) {
                remainingSumElement.textContent = `남은 합: ${remaining}`;
                generateButton.disabled = true;
            } else if (remaining === 0) {
                remainingSumElement.textContent = `남은 합: 0`;
                generateButton.disabled = false;
            } else {
                remainingSumElement.textContent = `남은 합: 초과`;
                generateButton.disabled = true;
            }
        }
    
        // Attach event listeners to inputs
        inputElements.forEach(input => {
            input.addEventListener('input', updateRemainingSum);
        });
    
        function convertToCustomFormat(value, positionName) {
            const digits = value.split('');
            const specialPositionIndex = getSpecialPositionIndex(positionName);

            return digits
                .map((digit, index) => {
                    if (index === specialPositionIndex) {
                        return "본"; // 해당 자리인 경우
                    }
                    return digit === "1" ? "폿" : "딜";
                })
                .join('');
        }

        function getSpecialPositionIndex(positionName) {
            const positionMap = {
                '1-1': 0, '1-2': 1, '1-3': 2, '1-4': 3,
                '2-1': 0, '2-2': 1, '2-3': 2, '2-4': 3,
                '3-1': 0, '3-2': 1, '3-3': 2, '3-4': 3,
                '4-1': 0, '4-2': 1, '4-3': 2, '4-4': 3
            };
            return positionMap[positionName];
        }

        generateButton.addEventListener('click', () => {
            const results = [];

            inputElements.forEach((input, index) => {
                const inputValue = parseInt(input.value) || 0;
                const isChecked = checkboxElements[index].checked;
                results.push(generateFilteredCombinations(inputValue, index, isChecked));
            });

            console.log("Generated combinations:", results); // 디버깅 로그

            const foundCombination = findFirstValidCombination(results);

            if (foundCombination) {
                const mappedResult = foundCombination
                    .map((value, index) => {
                        const positionName = generatePositionName(index + 1);
                        return `${positionName} ${convertToCustomFormat(value, positionName)}`;
                    })
                    .join('/');
                resultSection.innerHTML = `<h3>유효 조합:</h3><p>${mappedResult}</p>`;
            } else {
                resultSection.innerHTML = `<h3>조건을 만족하는 조합을 찾을 수 없습니다.</h3>`;
            }
        });
    
        // 가능한 조합 중 첫 번째 유효한 조합을 찾는 함수
        function findFirstValidCombination(arrays) {
            const maxDigitSum = 4;
            let found = null;
    
            function cartesianProductRecursive(depth, combination) {
                if (depth === arrays.length) {
                    const digitSums = combination.reduce((sums, current) => {
                        const digits = current.split('').map(Number);
                        return digits.map((digit, index) => (sums[index] || 0) + digit);
                    }, []);
                    if (digitSums.every(sum => sum === maxDigitSum)) {
                        found = combination;
                        return true;
                    }
                    return false;
                }
    
                for (const value of arrays[depth]) {
                    if (cartesianProductRecursive(depth + 1, [...combination, value])) {
                        return true;
                    }
                }
                return false;
            }
    
            cartesianProductRecursive(0, []);
            return found;
        }
    
        // 조합 생성 함수 (수정된 부분)
        function generateFilteredCombinations(inputValue, positionIndex, isChecked) {
            const combinations = [];
            const totalPositions = 4;
            const baseArray = Array(totalPositions).fill(0);

            if (isChecked) {
                // 체크된 경우: 해당 자리를 1로 고정
                baseArray[positionIndex % totalPositions] = 1;

                const remainingValue = inputValue - 1;
                if (remainingValue >= 0) {
                    const indices = Array.from({ length: totalPositions }, (_, i) => i).filter(i => i !== positionIndex % totalPositions);
                    const subsets = getFilteredSubsets(indices, remainingValue);

                    subsets.forEach(subset => {
                        const combination = [...baseArray];
                        subset.forEach(index => {
                            combination[index] = 1;
                        });
                        combinations.push(combination.join(''));
                    });
                } else {
                    combinations.push(baseArray.join(''));
                }
            } else {
                // 체크되지 않은 경우: 해당 자리를 0으로 고정
                baseArray[positionIndex % totalPositions] = 0;

                const indices = Array.from({ length: totalPositions }, (_, i) => i).filter(i => i !== positionIndex % totalPositions);
                const subsets = getFilteredSubsets(indices, inputValue);

                subsets.forEach(subset => {
                    const combination = [...baseArray];
                    subset.forEach(index => {
                        combination[index] = 1;
                    });
                    combinations.push(combination.join(''));
                });
            }

            return combinations;
        }
    
        // 최적화된 부분 집합 생성 함수
        function getFilteredSubsets(array, size) {
            if (size === 0) return [[]];
            if (array.length === 0) return [];
            const [first, ...rest] = array;
    
            const includeFirst = getFilteredSubsets(rest, size - 1).map(subset => [first, ...subset]);
            const excludeFirst = getFilteredSubsets(rest, size);
    
            return [...includeFirst, ...excludeFirst];
        }
    
        // 위치 이름 생성
        function generatePositionName(index) {
            const row = Math.ceil(index / 4);
            const col = index % 4 === 0 ? 4 : index % 4;
            return `${row}-${col}`;
        }
    
        // Reset all inputs and checkboxes
        resetButton.addEventListener('click', () => {
            inputElements.forEach(input => input.value = '0');
            checkboxElements.forEach(checkbox => checkbox.checked = false);
            resultSection.innerHTML = '<p></p>';
        });
    
        // Initial call to set the remaining sum
        updateRemainingSum();
    </script>
</body>
</html>
