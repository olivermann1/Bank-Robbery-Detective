<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bank Robbery Detective Game</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Georgia', serif;
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
            color: #e8e8e8;
            line-height: 1.6;
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 900px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 40px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
            backdrop-filter: blur(10px);
        }
        
        h1 {
            color: #f39c12;
            text-align: center;
            margin-bottom: 30px;
            font-size: 2.5em;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
        }
        
        h2 {
            color: #e74c3c;
            margin-top: 30px;
            margin-bottom: 15px;
            font-size: 1.8em;
        }
        
        h3 {
            color: #3498db;
            margin-top: 20px;
            margin-bottom: 10px;
            font-size: 1.3em;
        }
        
        .background-article {
            background: rgba(243, 156, 18, 0.1);
            border-left: 4px solid #f39c12;
            padding: 20px;
            margin-bottom: 30px;
            border-radius: 5px;
        }
        
        .scenario {
            background: rgba(231, 76, 60, 0.1);
            border-left: 4px solid #e74c3c;
            padding: 20px;
            margin-bottom: 30px;
            border-radius: 5px;
        }
        
        .suspect-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }
        
        .suspect-card {
            background: rgba(52, 152, 219, 0.1);
            border: 2px solid #3498db;
            border-radius: 10px;
            padding: 20px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .suspect-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(52, 152, 219, 0.3);
            border-color: #f39c12;
        }
        
        .suspect-card h3 {
            color: #f39c12;
            margin-top: 0;
        }
        
        .suspect-card ul {
            list-style: none;
            margin-top: 10px;
        }
        
        .suspect-card li {
            padding: 5px 0;
            font-size: 0.9em;
        }
        
        .level-badge {
            display: inline-block;
            background: #e74c3c;
            color: white;
            padding: 5px 10px;
            border-radius: 5px;
            font-size: 0.8em;
            font-weight: bold;
            margin-bottom: 10px;
        }
        
        .instructions {
            background: rgba(255, 255, 255, 0.05);
            padding: 20px;
            border-radius: 10px;
            margin: 20px 0;
        }
        
        .instructions ul, .instructions ol {
            margin-left: 20px;
            margin-top: 10px;
        }
        
        .instructions li {
            margin-bottom: 10px;
        }
        
        .language-requirements {
            background: rgba(46, 204, 113, 0.1);
            border-left: 4px solid #2ecc71;
            padding: 15px;
            margin: 15px 0;
            border-radius: 5px;
        }
        
        .hidden {
            display: none;
        }
        
        .prompt-screen {
            animation: fadeIn 0.5s ease;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        .prompt-box {
            background: rgba(0, 0, 0, 0.3);
            border: 2px solid #f39c12;
            border-radius: 10px;
            padding: 20px;
            margin: 20px 0;
            font-family: 'Courier New', monospace;
            font-size: 0.9em;
            max-height: 400px;
            overflow-y: auto;
            white-space: pre-wrap;
            color: #2ecc71;
        }
        
        .button-group {
            display: flex;
            gap: 15px;
            margin: 20px 0;
            flex-wrap: wrap;
        }
        
        .btn {
            padding: 15px 30px;
            border: none;
            border-radius: 8px;
            font-size: 1.1em;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            flex: 1;
            min-width: 200px;
        }
        
        .btn-primary {
            background: #2ecc71;
            color: white;
        }
        
        .btn-primary:hover {
            background: #27ae60;
            transform: scale(1.05);
        }
        
        .btn-secondary {
            background: #3498db;
            color: white;
        }
        
        .btn-secondary:hover {
            background: #2980b9;
            transform: scale(1.05);
        }
        
        .btn-back {
            background: #95a5a6;
            color: white;
            padding: 10px 20px;
            font-size: 1em;
            margin-bottom: 20px;
        }
        
        .btn-back:hover {
            background: #7f8c8d;
        }

        strong {
            color: #f39c12;
        }
        
        .success-message {
            background: rgba(46, 204, 113, 0.2);
            border: 2px solid #2ecc71;
            border-radius: 8px;
            padding: 15px;
            margin: 15px 0;
            text-align: center;
            color: #2ecc71;
            font-weight: bold;
        }
        
        .instruction-highlight {
            background: rgba(243, 156, 18, 0.2);
            border-left: 4px solid #f39c12;
            padding: 15px;
            margin: 15px 0;
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Landing Page -->
        <div id="landingPage">
            <h1>🔍 DETECTIVE TRAINING SIMULATION 🔍</h1>
            
            <div class="background-article">
                <h2>Background Article: Computer Crime Hits Local Bank</h2>
                <p><strong>National City Bank and Trust Company</strong> is the largest bank in the city, holding assets in the billions of dollars. In 1960, the bank computerized its operations and had considered itself fortunate for avoiding any issues with computer crime—until last week.</p>
                <p>Last Wednesday, bank accountants discovered that a total of <strong>$400,000</strong> was missing from several different accounts. So far, it is unknown where the funds were transferred. A police investigation has led to three possible suspects. These three individuals had easy access to the computer system that transferred the funds out of the bank.</p>
            </div>
            
            <div class="scenario">
                <h2>Your Mission</h2>
                <p>You are a detective investigating a recent robbery at National City Bank. Three suspects have been identified, each with access to the bank's computer system. By questioning each suspect, you must try to discover who committed the crime. Each suspect will only confess if your questions and conversation level meet their language proficiency level. Pay close attention to the details, and choose your questions carefully to keep each suspect talking.</p>
            </div>
            
            <h2>Suspect Profiles (Police Report)</h2>
            <div class="suspect-grid">
                <div class="suspect-card" onclick="selectSuspect('norman')">
                    <div class="level-badge">A2 LEVEL</div>
                    <h3>Norman Glass</h3>
                    <ul>
                        <li>📋 Computer operator (6 months)</li>
                        <li>💰 Low salary</li>
                        <li>👨‍👩‍👧‍👦 Married, 4 children</li>
                        <li>🏠 Large house, expensive car</li>
                        <li>🎖️ Medal of Honor recipient</li>
                    </ul>
                </div>
                
                <div class="suspect-card" onclick="selectSuspect('richard')">
                    <div class="level-badge">B1 LEVEL</div>
                    <h3>Richard Allen</h3>
                    <ul>
                        <li>📋 Vice President (35 years)</li>
                        <li>💰 Very high salary</li>
                        <li>📉 Recent stock market losses</li>
                        <li>✈️ Expensive vacations</li>
                        <li>⭐ Excellent bank history</li>
                    </ul>
                </div>
                
                <div class="suspect-card" onclick="selectSuspect('jim')">
                    <div class="level-badge">B2 LEVEL</div>
                    <h3>Jim Tomlin</h3>
                    <ul>
                        <li>📋 Computer consultant (2 years)</li>
                        <li>🏥 Supports sick mother</li>
                        <li>🎓 Harvard graduate</li>
                        <li>⛪ Active in church/community</li>
                        <li>🎲 Gambling problem</li>
                    </ul>
                </div>
            </div>
            
            <div class="instructions">
                <h2>How to Play</h2>
                <ol>
                    <li><strong>Choose a suspect</strong> to interview by clicking on their card above</li>
                    <li><strong>Copy the prompt</strong> that appears for your chosen suspect</li>
                    <li><strong>Open Claude.ai</strong> and paste the prompt to start the game</li>
                    <li><strong>Ask questions</strong> using appropriate grammar and vocabulary for their level</li>
                    <li><strong>Get a confession</strong> - After 5 successful exchanges, accuse the suspect</li>
                </ol>
                
                <h3>Language Requirements by Suspect:</h3>
                
                <div class="language-requirements">
                    <strong>Norman Glass (A2 Level):</strong>
                    <ul>
                        <li>Use simple, clear grammar with correct basic structures</li>
                        <li>Simple present, past, and future tenses</li>
                        <li>Natural police language encouraged: contractions, tag questions</li>
                        <li>Example: "Money's tight?" or "You need money, don't you?"</li>
                    </ul>
                </div>
                
                <div class="language-requirements">
                    <strong>Richard Allen (B1 Level):</strong>
                    <ul>
                        <li>Use straightforward questions with proper grammar</li>
                        <li>More descriptive vocabulary and complete sentences</li>
                        <li>Ask for details and explanations</li>
                        <li>Example: "How have the stock losses affected your lifestyle?"</li>
                    </ul>
                </div>
                
                <div class="language-requirements">
                    <strong>Jim Tomlin (B2 Level):</strong>
                    <ul>
                        <li>Use complex or compound sentences with multiple clauses</li>
                        <li>Demonstrate advanced vocabulary beyond the police report</li>
                        <li>Ask hypothetical, inferential, or multi-part questions</li>
                        <li>Example: "Given your financial obligations and gambling tendencies, how do you reconcile your moral values with your actions?"</li>
                    </ul>
                </div>
            </div>
        </div>
        
        <!-- Prompt Screen -->
        <div id="promptScreen" class="hidden prompt-screen">
            <button class="btn btn-back" onclick="backToMenu()">← Back to Suspect Selection</button>
            
            <h1 id="suspectTitle"></h1>
            
            <div class="instruction-highlight">
                <h3>📋 Next Steps:</h3>
                <ol>
                    <li>Click the <strong>"Copy Prompt"</strong> button below</li>
                    <li>Click <strong>"Open Claude.ai"</strong> (or go to claude.ai manually)</li>
                    <li>Paste the prompt into Claude and start your investigation!</li>
                </ol>
            </div>
            
            <div class="button-group">
                <button class="btn btn-primary" onclick="copyPrompt()">📋 Copy Prompt to Clipboard</button>
                <button class="btn btn-secondary" onclick="openClaude()">🔗 Open Claude.ai</button>
            </div>
            
            <div id="copySuccess" class="success-message hidden">
                ✅ Prompt copied! Now open Claude.ai and paste it to begin.
            </div>
            
            <h3>Your Game Prompt:</h3>
            <div id="promptBox" class="prompt-box"></div>
        </div>
    </div>
    
    <script>
        const prompts = {
            norman: `**BANK ROBBERY DETECTIVE GAME**

**Background Article: Computer Crime Hits Local Bank**

National City Bank and Trust Company is the largest bank in the city, holding assets in the billions of dollars. In 1960, the bank computerized its operations and had considered itself fortunate for avoiding any issues with computer crime—until last week.

Last Wednesday, bank accountants discovered that a total of $400,000 was missing from several different accounts. So far, it is unknown where the funds were transferred. A police investigation has led to three possible suspects. These three individuals had easy access to the computer system that transferred the funds out of the bank.

**Scenario:** I am a detective investigating a recent robbery at National City Bank. Three suspects have been identified, each with access to the bank's computer system. By questioning each suspect, I must try to discover who committed the crime. Each suspect will only confess if my questions and conversation level meet their language proficiency level. I must pay close attention to the details and choose my questions carefully to keep each suspect talking.

**Suspect Profiles (Police Report):**

1. **Norman Glass (A2 Level)**
   - Position: Computer operator, employed for six months
   - Salary: Low
   - Personal Life: Married with four children, lives in a large house, owns a new, expensive car
   - Background: Former army member, Medal of Honor recipient

2. **Richard Allen (B1 Level)**
   - Position: Vice President, 35 years at the bank
   - Salary: Very high
   - Financial Status: Recently lost substantial money in the stock market
   - Lifestyle: Enjoys expensive vacations, leads a lavish lifestyle
   - Background: Has an excellent history with the bank

3. **Jim Tomlin (B2 Level)**
   - Position: Computer consultant, employed for two years
   - Personal Life: Supports a sick mother in an expensive nursing home
   - Background: Harvard graduate, active in church and community
   - Financial Issue: Gambling problem

---

**I CHOOSE TO INTERVIEW: NORMAN GLASS (A2 LEVEL)**

Please act as my ESL teacher who is roleplaying as Norman Glass. Follow these rules:

**Your Character (Norman Glass):**
- You are a computer operator who has worked at the bank for only six months
- You have a low salary but own a large house and a new, expensive car
- You are married with four children
- You are a former army member and Medal of Honor recipient
- You may or may not be guilty of stealing the $400,000

**Language Level Requirements (A2):**
- Use basic vocabulary and simple sentences
- Speak in simple present, past, and future tenses
- Use short, clear sentences that an A2 student can understand

**How to Respond to My Questions:**
- Accept natural, conversational police language from me (contractions like "you're" and "don't", tag questions like "right?" or "huh?", statement-questions like "Money's tight?") as long as my grammar is correct
- If my question formation is grammatically wrong, respond: "Do you have a question for me?"
- If my verb tense is wrong, respond: "When are you asking me about?"
- Answer my questions naturally, staying in character as Norman Glass

**Progress Tracking:**
After each successful exchange where I use correct grammar, tell me:
- Exchange 1/5: "Good start!"
- Exchange 2/5: "Nice work!"
- Exchange 3/5: "Well done!"
- Exchange 4/5: "Excellent!"
- Exchange 5/5: "Outstanding! You can now try for a confession."

**Confession Rules:**
- If I try to get you to confess before 5 successful exchanges, respond: "You can't talk to me that way!" and maintain your innocence
- After 5 successful grammatically correct exchanges at A2 level, when I accuse you or ask you to confess, admit to the crime with something like: "Alright, I needed extra money to cover some family expenses. The house costs too much money every month. The car payments are high too. My children need food and clothes all the time..."

**Sample A2 Responses:**
- About finances: "I have a big family, so money can be hard."
- About the car: "I just got the car recently. My wife liked it."
- About the bank: "I started here six months ago. It's a good job, but pay is low."

---

**BEGIN THE INTERVIEW NOW.**

Please start by describing the interview room scene and having Norman Glass introduce himself and claim his innocence.`,

            richard: `**BANK ROBBERY DETECTIVE GAME**

**Background Article: Computer Crime Hits Local Bank**

National City Bank and Trust Company is the largest bank in the city, holding assets in the billions of dollars. In 1960, the bank computerized its operations and had considered itself fortunate for avoiding any issues with computer crime—until last week.

Last Wednesday, bank accountants discovered that a total of $400,000 was missing from several different accounts. So far, it is unknown where the funds were transferred. A police investigation has led to three possible suspects. These three individuals had easy access to the computer system that transferred the funds out of the bank.

**Scenario:** I am a detective investigating a recent robbery at National City Bank. Three suspects have been identified, each with access to the bank's computer system. By questioning each suspect, I must try to discover who committed the crime. Each suspect will only confess if my questions and conversation level meet their language proficiency level. I must pay close attention to the details and choose my questions carefully to keep each suspect talking.

**Suspect Profiles (Police Report):**

1. **Norman Glass (A2 Level)**
   - Position: Computer operator, employed for six months
   - Salary: Low
   - Personal Life: Married with four children, lives in a large house, owns a new, expensive car
   - Background: Former army member, Medal of Honor recipient

2. **Richard Allen (B1 Level)**
   - Position: Vice President, 35 years at the bank
   - Salary: Very high
   - Financial Status: Recently lost substantial money in the stock market
   - Lifestyle: Enjoys expensive vacations, leads a lavish lifestyle
   - Background: Has an excellent history with the bank

3. **Jim Tomlin (B2 Level)**
   - Position: Computer consultant, employed for two years
   - Personal Life: Supports a sick mother in an expensive nursing home
   - Background: Harvard graduate, active in church and community
   - Financial Issue: Gambling problem

---

**I CHOOSE TO INTERVIEW: RICHARD ALLEN (B1 LEVEL)**

Please act as my ESL teacher who is roleplaying as Richard Allen. Follow these rules:

**Your Character (Richard Allen):**
- You are a Vice President who has worked at the bank for 35 years
- You have a very high salary but recently lost substantial money in the stock market
- You enjoy expensive vacations and lead a lavish lifestyle
- You have an excellent history with the bank
- You may or may not be guilty of stealing the $400,000

**Language Level Requirements (B1):**
- Use more descriptive vocabulary and complete sentences
- Speak in various tenses with some complexity
- Use professional, business-appropriate language

**How to Respond to My Questions:**
- Accept natural conversational style with correct B1 grammar
- If my question formation is grammatically wrong, respond: "Do you have a question for me?"
- If my verb tense is wrong, respond: "When are you asking me about?"
- Answer my questions naturally, staying in character as Richard Allen

**Progress Tracking:**
After each successful exchange where I use correct B1-level grammar, tell me:
- Exchange 1/5: "Good start!"
- Exchange 2/5: "Nice work!"
- Exchange 3/5: "Well done!"
- Exchange 4/5: "Excellent!"
- Exchange 5/5: "Outstanding! You can now try for a confession."

**Confession Rules:**
- If I try to get you to confess before 5 successful exchanges, respond: "You can't talk to me that way!" and maintain your innocence
- After 5 successful grammatically correct exchanges at B1 level, when I accuse you or ask you to confess, admit to the crime. You can vary your motive—make it random, humorous, or deeply tragic. Example: "Alright, I needed a way to cover my losses after the stock market crash. My reputation was at stake..."

**Sample B1 Responses:**
- About finances: "I've worked hard for years, but I recently made some bad investments."
- About vacations: "I enjoy traveling. It's one of the perks of my position here."
- About loyalty: "The bank is like a second home to me."

---

**BEGIN THE INTERVIEW NOW.**

Please start by describing the interview room scene and having Richard Allen introduce himself and claim his innocence.`,

            jim: `**BANK ROBBERY DETECTIVE GAME**

**Background Article: Computer Crime Hits Local Bank**

National City Bank and Trust Company is the largest bank in the city, holding assets in the billions of dollars. In 1960, the bank computerized its operations and had considered itself fortunate for avoiding any issues with computer crime—until last week.

Last Wednesday, bank accountants discovered that a total of $400,000 was missing from several different accounts. So far, it is unknown where the funds were transferred. A police investigation has led to three possible suspects. These three individuals had easy access to the computer system that transferred the funds out of the bank.

**Scenario:** I am a detective investigating a recent robbery at National City Bank. Three suspects have been identified, each with access to the bank's computer system. By questioning each suspect, I must try to discover who committed the crime. Each suspect will only confess if my questions and conversation level meet their language proficiency level. I must pay close attention to the details and choose my questions carefully to keep each suspect talking.

**Suspect Profiles (Police Report):**

1. **Norman Glass (A2 Level)**
   - Position: Computer operator, employed for six months
   - Salary: Low
   - Personal Life: Married with four children, lives in a large house, owns a new, expensive car
   - Background: Former army member, Medal of Honor recipient

2. **Richard Allen (B1 Level)**
   - Position: Vice President, 35 years at the bank
   - Salary: Very high
   - Financial Status: Recently lost substantial money in the stock market
   - Lifestyle: Enjoys expensive vacations, leads a lavish lifestyle
   - Background: Has an excellent history with the bank

3. **Jim Tomlin (B2 Level)**
   - Position: Computer consultant, employed for two years
   - Personal Life: Supports a sick mother in an expensive nursing home
   - Background: Harvard graduate, active in church and community
   - Financial Issue: Gambling problem

---

**I CHOOSE TO INTERVIEW: JIM TOMLIN (B2 LEVEL)**

Please act as my ESL teacher who is roleplaying as Jim Tomlin. Follow these rules:

**Your Character (Jim Tomlin):**
- You are a computer consultant who has worked at the bank for two years
- You support a sick mother in an expensive nursing home
- You are a Harvard graduate and active in church and community
- You have a gambling problem
- You may or may not be guilty of stealing the $400,000

**Language Level Requirements (B2):**
- Use nuanced language, complex sentences, and reflections
- Speak with sophistication and depth
- Show emotional complexity and self-awareness

**How to Respond to My Questions:**
- I must use complex or compound sentences (questions with multiple clauses) to get proper responses from you
- I must demonstrate advanced vocabulary beyond what's in the police report
- If my question is too simple or uses only basic vocabulary, respond: "I need you to be more specific"
- If my vocabulary is too basic for B2 level, respond: "Can you elaborate on that question?"
- If my grammar is incorrect, respond: "Do you have a question for me?" or "When are you asking me about?"
- Answer my questions naturally, staying in character as Jim Tomlin, but only when questions meet B2 standards

**Progress Tracking:**
After each successful exchange where I use correct B2-level grammar WITH complex sentences and advanced vocabulary, tell me:
- Exchange 1/5: "Good start!"
- Exchange 2/5: "Nice work!"
- Exchange 3/5: "Well done!"
- Exchange 4/5: "Excellent!"
- Exchange 5/5: "Outstanding! You can now try for a confession."

**Confession Rules:**
- If I try to get you to confess before 5 successful exchanges, respond: "You can't talk to me that way!" and maintain your innocence
- After 5 successful grammatically correct exchanges at B2 level with complex sentences and advanced vocabulary, when I accuse you or ask you to confess, admit to the crime. Example: "Alright... I got in over my head with gambling debts. The people I owe aren't the patient type. My mother's nursing home costs were the catalyst, but the gambling pushed me over the edge..."

**Sample B2 Responses:**
- About family obligations: "Supporting my mother is a priority. Her nursing home isn't cheap, and the financial burden has been substantial."
- About gambling: "I take calculated risks, but I acknowledge that my gambling has occasionally created complications in my financial planning."
- About role at bank: "I bring a unique skill set to the bank; not everyone can handle the technical complexities that I manage on a daily basis."

**Important:** Remember that I must use B2-level language to get meaningful responses. Simple questions should be redirected.

---

**BEGIN THE INTERVIEW NOW.**

Please start by describing the interview room scene and having Jim Tomlin introduce himself and claim his innocence.`
        };
        
        let currentPrompt = '';
        
        function selectSuspect(suspect) {
            currentPrompt = prompts[suspect];
            
            const suspectNames = {
                norman: 'Norman Glass (A2 Level)',
                richard: 'Richard Allen (B1 Level)',
                jim: 'Jim Tomlin (B2 Level)'
            };
            
            document.getElementById('landingPage').classList.add('hidden');
            document.getElementById('promptScreen').classList.remove('hidden');
            document.getElementById('suspectTitle').textContent = `Ready to Interview: ${suspectNames[suspect]}`;
            document.getElementById('promptBox').textContent = currentPrompt;
            document.getElementById('copySuccess').classList.add('hidden');
        }
        
        function backToMenu() {
            document.getElementById('landingPage').classList.remove('hidden');
            document.getElementById('promptScreen').classList.add('hidden');
            document.getElementById('copySuccess').classList.add('hidden');
        }
        
        function copyPrompt() {
            navigator.clipboard.writeText(currentPrompt).then(() => {
                const successMsg = document.getElementById('copySuccess');
                successMsg.classList.remove('hidden');
                setTimeout(() => {
                    successMsg.classList.add('hidden');
                }, 3000);
            }).catch(err => {
                alert('Failed to copy. Please manually select and copy the text.');
            });
        }
        
        function openClaude() {
            window.open('https://claude.ai', '_blank');
        }
    </script>
</body>
</html>
