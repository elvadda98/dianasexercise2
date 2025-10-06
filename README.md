<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: Everyday Words</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #6a93cb 0%, #a4bfef 100%);
            min-height: 100vh;
            padding: 20px;
            color: #2c3e50;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            max-width: 1000px;
            width: 100%;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #f5f7fa, #e8f4f2);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .word-bank h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(74, 111, 165, 0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(74, 111, 165, 0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .option {
            padding: 15px 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .option:hover {
            border-color: #4a6fa5;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .option.selected {
            background: #4a6fa5;
            color: white;
            border-color: #4a6fa5;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #4a6fa5;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #4a6fa5;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .match-item.selected {
            background: #e8f4f2;
            border-color: #4a6fa5;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .reset-btn {
            background: linear-gradient(135deg, #f44336, #ff7961);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 10px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(244, 67, 54, 0.3);
        }

        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(244, 67, 54, 0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
            z-index: 1000;
        }

        .icon {
            font-size: 24px;
            margin-right: 10px;
            vertical-align: middle;
        }

        /* Vocabulary List Styles */
        .vocabulary-list {
            padding: 20px;
        }

        .vocabulary-item {
            margin-bottom: 25px;
            padding: 20px;
            border-radius: 10px;
            background: #f8f9fa;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }

        .vocabulary-item h3 {
            color: #4a6fa5;
            margin-bottom: 10px;
            font-size: 1.4em;
            border-bottom: 2px solid #4a6fa5;
            padding-bottom: 8px;
        }

        .vocabulary-item p {
            margin-bottom: 8px;
            line-height: 1.6;
        }

        .example {
            font-style: italic;
            color: #555;
            padding-left: 15px;
            border-left: 3px solid #4a6fa5;
            margin-top: 10px;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 200px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/12</div>
    
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-book icon"></i> Vocabulary Game: Everyday Words</h1>
            <p>Test your knowledge of these common English terms!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('vocabulary')">Vocabulary List</button>
            <button class="nav-btn" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Definitions</button>
            <button class="nav-btn" onclick="showSection('multiple-choice')">Multiple Choice</button>
        </div>

        <!-- Vocabulary List Section -->
        <div id="vocabulary" class="game-section active">
            <h2 style="text-align: center; margin-bottom: 20px; color: #4a6fa5;">Vocabulary Explanations</h2>
            
            <div class="vocabulary-list">
                <div class="vocabulary-item">
                    <h3>habit</h3>
                    <p><strong>Definition:</strong> A settled or regular tendency or practice, especially one that is hard to give up.</p>
                    <p><strong>Usage:</strong> Often refers to behaviors that are done regularly and automatically.</p>
                    <p class="example"><strong>Example:</strong> "Brushing your teeth twice a day is a good habit."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>on top</h3>
                    <p><strong>Definition:</strong> In a position of control, authority, or success; managing a situation well.</p>
                    <p><strong>Usage:</strong> Can also literally mean on the highest point or surface of something.</p>
                    <p class="example"><strong>Example:</strong> "Despite the challenges, she stayed on top of her work."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>useless</h3>
                    <p><strong>Definition:</strong> Not fulfilling or not able to fulfill the intended purpose; having no ability or skill in a specified activity or area.</p>
                    <p><strong>Usage:</strong> Describes something that doesn't work or has no practical value.</p>
                    <p class="example"><strong>Example:</strong> "This broken phone is completely useless."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>bark</h3>
                    <p><strong>Definition:</strong> The sharp explosive cry of a dog, fox, or similar animal; the tough protective outer covering of a tree.</p>
                    <p><strong>Usage:</strong> Has two common meanings - animal sound and tree covering.</p>
                    <p class="example"><strong>Example:</strong> "The dog began to bark at the mail carrier."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>dry</h3>
                    <p><strong>Definition:</strong> Free from moisture or liquid; not wet or moist.</p>
                    <p><strong>Usage:</strong> Can describe weather, objects, or even humor.</p>
                    <p class="example"><strong>Example:</strong> "Hang your wet clothes outside to dry in the sun."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>company</h3>
                    <p><strong>Definition:</strong> A commercial business; the fact or condition of being with another or others.</p>
                    <p><strong>Usage:</strong> Has both business and social meanings.</p>
                    <p class="example"><strong>Example:</strong> "She started her own company last year."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>vacuum</h3>
                    <p><strong>Definition:</strong> A space entirely devoid of matter; an electrical appliance that cleans by suction.</p>
                    <p><strong>Usage:</strong> Scientific term or common household appliance.</p>
                    <p class="example"><strong>Example:</strong> "I need to vacuum the living room carpet."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>broom</h3>
                    <p><strong>Definition:</strong> A long-handled brush of bristles or twigs used for sweeping.</p>
                    <p><strong>Usage:</strong> Common cleaning tool found in most households.</p>
                    <p class="example"><strong>Example:</strong> "She swept the floor with an old broom."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>steal</h3>
                    <p><strong>Definition:</strong> To take another person's property without permission or legal right.</p>
                    <p><strong>Usage:</strong> Can also mean to move somewhere quietly or surreptitiously.</p>
                    <p class="example"><strong>Example:</strong> "It is wrong to steal from others."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>slow</h3>
                    <p><strong>Definition:</strong> Moving or operating at a low speed; not quick.</p>
                    <p><strong>Usage:</strong> Can describe speed, mental processing, or progress.</p>
                    <p class="example"><strong>Example:</strong> "The traffic was moving very slow this morning."</p>
                </div>
            </div>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">habit</span>
                    <span class="word-option">on top</span>
                    <span class="word-option">useless</span>
                    <span class="word-option">bark</span>
                    <span class="word-option">dry</span>
                    <span class="word-option">company</span>
                    <span class="word-option">vacuum</span>
                    <span class="word-option">broom</span>
                    <span class="word-option">steal</span>
                    <span class="word-option">slow</span>
                </div>
            </div>

            <div id="fill-gaps-container">
                <!-- Sentences will be dynamically inserted here -->
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
            <button class="reset-btn" onclick="resetFillBlanks()">Reset Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #4a6fa5;">Match the words with their definitions</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Vocabulary Words</h4>
                    <div class="match-item" data-word="habit" onclick="selectMatch(this)">habit</div>
                    <div class="match-item" data-word="on top" onclick="selectMatch(this)">on top</div>
                    <div class="match-item" data-word="useless" onclick="selectMatch(this)">useless</div>
                    <div class="match-item" data-word="bark" onclick="selectMatch(this)">bark</div>
                    <div class="match-item" data-word="dry" onclick="selectMatch(this)">dry</div>
                    <div class="match-item" data-word="company" onclick="selectMatch(this)">company</div>
                    <div class="match-item" data-word="vacuum" onclick="selectMatch(this)">vacuum</div>
                    <div class="match-item" data-word="broom" onclick="selectMatch(this)">broom</div>
                    <div class="match-item" data-word="steal" onclick="selectMatch(this)">steal</div>
                    <div class="match-item" data-word="slow" onclick="selectMatch(this)">slow</div>
                </div>
                <div class="match-column">
                    <h4>Definitions</h4>
                    <div id="meanings-container">
                        <!-- Meanings will be dynamically inserted here -->
                    </div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
            <button class="check-btn" onclick="checkMatching()">Check Matching</button>
            <button class="reset-btn" onclick="resetMatching()">Reset Matching</button>
        </div>

        <!-- Multiple Choice Section -->
        <div id="multiple-choice" class="game-section">
            <div class="question">
                <h3>Question 1: What does "habit" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A type of clothing</div>
                    <div class="option" onclick="selectOption(this, true)">A regular practice or tendency</div>
                    <div class="option" onclick="selectOption(this, false)">A small house</div>
                    <div class="option" onclick="selectOption(this, false)">A type of food</div>
                </div>
                <div class="feedback" id="mc-feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2: "On top" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Underneath something</div>
                    <div class="option" onclick="selectOption(this, true)">In control or managing well</div>
                    <div class="option" onclick="selectOption(this, false)">Feeling sad or depressed</div>
                    <div class="option" onclick="selectOption(this, false)">Moving quickly</div>
                </div>
                <div class="feedback" id="mc-feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3: Something that is "useless":</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Works perfectly</div>
                    <div class="option" onclick="selectOption(this, true)">Has no practical value or function</div>
                    <div class="option" onclick="selectOption(this, false)">Is very expensive</div>
                    <div class="option" onclick="selectOption(this, false)">Is brand new</div>
                </div>
                <div class="feedback" id="mc-feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4: "Bark" can refer to:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A type of fruit</div>
                    <div class="option" onclick="selectOption(this, true)">A dog's sound or tree covering</div>
                    <div class="option" onclick="selectOption(this, false)">A musical instrument</div>
                    <div class="option" onclick="selectOption(this, false)">A type of vehicle</div>
                </div>
                <div class="feedback" id="mc-feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5: "Dry" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Wet or moist</div>
                    <div class="option" onclick="selectOption(this, true)">Free from moisture or liquid</div>
                    <div class="option" onclick="selectOption(this, false)">Very cold</div>
                    <div class="option" onclick="selectOption(this, false)">Extremely hot</div>
                </div>
                <div class="feedback" id="mc-feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6: "Company" can mean:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Being alone</div>
                    <div class="option" onclick="selectOption(this, true)">A business or being with others</div>
                    <div class="option" onclick="selectOption(this, false)">A type of food</div>
                    <div class="option" onclick="selectOption(this, false)">A vehicle</div>
                </div>
                <div class="feedback" id="mc-feedback-6" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 7: A "vacuum" is:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A cooking appliance</div>
                    <div class="option" onclick="selectOption(this, true)">A cleaning appliance or space without matter</div>
                    <div class="option" onclick="selectOption(this, false)">A type of furniture</div>
                    <div class="option" onclick="selectOption(this, false)">A musical instrument</div>
                </div>
                <div class="feedback" id="mc-feedback-7" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 8: A "broom" is used for:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Cooking</div>
                    <div class="option" onclick="selectOption(this, true)">Sweeping floors</div>
                    <div class="option" onclick="selectOption(this, false)">Writing</div>
                    <div class="option" onclick="selectOption(this, false)">Painting</div>
                </div>
                <div class="feedback" id="mc-feedback-8" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 9: To "steal" means to:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Give something away</div>
                    <div class="option" onclick="selectOption(this, true)">Take something without permission</div>
                    <div class="option" onclick="selectOption(this, false)">Buy something legally</div>
                    <div class="option" onclick="selectOption(this, false)">Share something with others</div>
                </div>
                <div class="feedback" id="mc-feedback-9" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 10: "Slow" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Moving at high speed</div>
                    <div class="option" onclick="selectOption(this, true)">Moving at low speed</div>
                    <div class="option" onclick="selectOption(this, false)">Stopping completely</div>
                    <div class="option" onclick="selectOption(this, false)">Moving backwards</div>
                </div>
                <div class="feedback" id="mc-feedback-10" style="display: none;"></div>
            </div>
            
            <button class="reset-btn" onclick="resetMultipleChoice()">Reset Answers</button>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];
        
        // Track correct answers for each section
        let fillBlanksCorrect = 0;
        let matchingCorrect = 0;
        let multipleChoiceCorrect = 0;
        
        // Definitions for the matching game
        const definitions = [
            { meaning: "habit", text: "A regular practice or tendency" },
            { meaning: "on top", text: "In control or managing well" },
            { meaning: "useless", text: "Having no practical value or function" },
            { meaning: "bark", text: "A dog's sound or tree covering" },
            { meaning: "dry", text: "Free from moisture or liquid" },
            { meaning: "company", text: "A business or being with others" },
            { meaning: "vacuum", text: "A cleaning appliance or empty space" },
            { meaning: "broom", text: "A tool used for sweeping floors" },
            { meaning: "steal", text: "To take something without permission" },
            { meaning: "slow", text: "Moving at a low speed" }
        ];

        // Sentences for the fill-in-the-blanks game
        const sentences = [
            { text: "Brushing your teeth twice a day is a good <input type='text' class='fill-blank' data-answer='habit' placeholder='answer'>.", answer: "habit" },
            { text: "Despite the challenges, she stayed <input type='text' class='fill-blank' data-answer='on top' placeholder='answer'> of her work.", answer: "on top" },
            { text: "This broken phone is completely <input type='text' class='fill-blank' data-answer='useless' placeholder='answer'>.", answer: "useless" },
            { text: "The dog began to <input type='text' class='fill-blank' data-answer='bark' placeholder='answer'> at the mail carrier.", answer: "bark" },
            { text: "Hang your wet clothes outside to <input type='text' class='fill-blank' data-answer='dry' placeholder='answer'> in the sun.", answer: "dry" },
            { text: "She started her own <input type='text' class='fill-blank' data-answer='company' placeholder='answer'> last year.", answer: "company" },
            { text: "I need to <input type='text' class='fill-blank' data-answer='vacuum' placeholder='answer'> the living room carpet.", answer: "vacuum" },
            { text: "She swept the floor with an old <input type='text' class='fill-blank' data-answer='broom' placeholder='answer'>.", answer: "broom" },
            { text: "It is wrong to <input type='text' class='fill-blank' data-answer='steal' placeholder='answer'> from others.", answer: "steal" },
            { text: "The traffic was moving very <input type='text' class='fill-blank' data-answer='slow' placeholder='answer'> this morning.", answer: "slow" },
            { text: "Smoking is a bad <input type='text' class='fill-blank' data-answer='habit' placeholder='answer'> that's hard to break.", answer: "habit" },
            { text: "The tree's rough <input type='text' class='fill-blank' data-answer='bark' placeholder='answer'> protected it from insects.", answer: "bark" },
            { text: "After the rain stopped, the roads began to <input type='text' class='fill-blank' data-answer='dry' placeholder='answer'>.", answer: "dry" },
            { text: "I enjoy your <input type='text' class='fill-blank' data-answer='company' placeholder='answer'> when we have coffee together.", answer: "company" }
        ];

        // Function to shuffle array (Fisher-Yates algorithm)
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        // Initialize the fill-in-the-blanks game with shuffled sentences
        function initFillBlanks() {
            const container = document.getElementById('fill-gaps-container');
            container.innerHTML = '';
            
            // Shuffle the sentences
            const shuffledSentences = shuffleArray([...sentences]);
            
            // Create and append the sentence elements
            shuffledSentences.forEach((sentence, index) => {
                const div = document.createElement('div');
                div.className = 'question';
                div.innerHTML = `
                    <h3>Question ${index + 1}:</h3>
                    <p>${sentence.text}</p>
                    <div class="feedback" id="feedback-${index + 1}" style="display: none;"></div>
                `;
                container.appendChild(div);
            });
        }

        // Initialize the matching game with shuffled definitions
        function initMatchingGame() {
            const meaningsContainer = document.getElementById('meanings-container');
            meaningsContainer.innerHTML = '';
            
            // Shuffle the definitions
            const shuffledDefinitions = shuffleArray([...definitions]);
            
            // Create and append the definition elements
            shuffledDefinitions.forEach(def => {
                const div = document.createElement('div');
                div.className = 'match-item';
                div.setAttribute('data-meaning', def.meaning);
                div.onclick = function() { selectMatch(this); };
                div.textContent = def.text;
                meaningsContainer.appendChild(div);
            });
        }

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
            
            // If showing fill-in-the-blanks section, reinitialize with shuffled sentences
            if (sectionId === 'fill-gaps') {
                initFillBlanks();
            }
            
            // If showing matching section, reinitialize with shuffled definitions
            if (sectionId === 'matching') {
                initMatchingGame();
                // Reset matching game state
                document.querySelectorAll('.match-item').forEach(item => {
                    item.classList.remove('selected', 'matched');
                });
                selectedWord = null;
                selectedMeaning = null;
                matchedPairs = [];
                document.getElementById('matching-feedback').style.display = 'none';
            }
            
            // Update score display
            updateScore();
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            fillBlanksCorrect = correctCount;
            updateScore();
        }

        function resetFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            blanks.forEach(blank => {
                blank.value = '';
                blank.classList.remove('correct', 'incorrect');
            });
            
            const feedbacks = document.querySelectorAll('#fill-gaps .feedback');
            feedbacks.forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            fillBlanksCorrect = 0;
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === definitions.length) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            matchingCorrect = matchedPairs.length;
            updateScore();
        }

        function checkMatching() {
            const allMatches = document.querySelectorAll('.match-item[data-word]');
            let allCorrect = true;
            
            allMatches.forEach(item => {
                if (!item.classList.contains('matched')) {
                    allCorrect = false;
                }
            });
            
            const feedback = document.getElementById('matching-feedback');
            if (allCorrect) {
                feedback.textContent = '🎉 Excellent! All matches are correct!';
                feedback.className = 'feedback correct';
            } else {
                const unmatchedCount = definitions.length - matchedPairs.length;
                feedback.textContent = `You have ${unmatchedCount} unmatched pair${unmatchedCount !== 1 ? 's' : ''}. Keep trying!`;
                feedback.className = 'feedback incorrect';
            }
            feedback.style.display = 'block';
        }

        function resetMatching() {
            document.querySelectorAll('.match-item').forEach(item => {
                item.classList.remove('selected', 'matched');
            });
            
            initMatchingGame();
            
            selectedWord = null;
            selectedMeaning = null;
            matchedPairs = [];
            
            document.getElementById('matching-feedback').style.display = 'none';
            
            matchingCorrect = 0;
            updateScore();
        }

        function selectOption(element, isCorrect) {
            // Remove selection from all options in this question
            const options = element.parentElement.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
                opt.classList.remove('correct');
                opt.classList.remove('incorrect');
            });
            
            // Mark the selected option
            element.classList.add('selected');
            
            const questionNumber = element.closest('.question').querySelector('h3').textContent.match(/\d+/)[0];
            const feedback = document.getElementById(`mc-feedback-${questionNumber}`);
            
            if (isCorrect) {
                element.classList.add('correct');
                feedback.textContent = '✅ Correct!';
                feedback.className = 'feedback correct';
            } else {
                element.classList.add('incorrect');
                feedback.textContent = '❌ Incorrect. Try again.';
                feedback.className = 'feedback incorrect';
                
                // Show the correct answer
                options.forEach(opt => {
                    if (opt.onclick.toString().includes('true')) {
                        opt.classList.add('correct');
                    }
                });
            }
            
            feedback.style.display = 'block';
            
            // Count correct answers in multiple choice
            multipleChoiceCorrect = document.querySelectorAll('#multiple-choice .option.correct.selected').length;
            updateScore();
        }

        function resetMultipleChoice() {
            document.querySelectorAll('#multiple-choice .option').forEach(option => {
                option.classList.remove('selected', 'correct', 'incorrect');
            });
            
            document.querySelectorAll('#multiple-choice .feedback').forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            multipleChoiceCorrect = 0;
            updateScore();
        }

        function updateScore() {
            // Total score
            score = fillBlanksCorrect + matchingCorrect + multipleChoiceCorrect;
            document.getElementById('score').textContent = score;
        }
        
        // Initialize the page
        window.onload = function() {
            initFillBlanks();
            initMatchingGame();
        }
    </script>
</body>
</html>
