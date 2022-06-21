<template>
<div>
<header>
            <h1>TypingGame</h1>
        </header>
        <div class="container">
            <p id="count"></p>
        <p id="time"></p>
        <h1>タイピングスキルを競おう!</h1>
        <h2>
            <p id="japanese"></p>
            <p id="romaji"></p>
        </h2>
        <table id="displayScore">
            <tr>
                <td class="label">スコア:</td>
                <td class="scoreArea"></td>
            </tr>
            <tr>
                <td class="label">正タイプ率:</td>
                <td class="scoreArea"></td>
            </tr>
            <tr>
                <td class="label">平均タイプ数:</td>
                <td class="scoreArea"></td>
            </tr>
        </table>

        <input type="button" id="start_button" value="スタート">
        <form id="limitForm" action="ranking.php" method="post">
            <p><label for="selectLimit">制限時間を選択</label></p>
            <select name="limit" id="selectLimit">
                <option value="30">30秒</option>
                <option value="60" selected>60秒</option>
                <option value="90">90秒</option>
            </select>
        </form>
        </div>
        </div>
</template>

<script>
    export default {
        mounted() {
            console.log('Component mounted.')
        }
    }
</script>
