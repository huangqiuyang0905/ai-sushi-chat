<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI苏轼 - 与东坡先生对话</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'SimSun', 'STSong', 'Microsoft YaHei', serif;
        }
        
        body {
            background-color: #f5f1e8;
            color: #333;
            min-height: 100vh;
            overflow-x: hidden;
            background-image: url("data:image/svg+xml,%3Csvg width='100' height='100' viewBox='0 0 100 100' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M11 18c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm48 25c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm-43-7c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm63 31c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM34 90c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm56-76c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM12 86c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm28-65c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm23-11c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-6 60c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm29 22c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zM32 63c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm57-13c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-9-21c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM60 91c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM35 41c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2z' fill='%23a1887f' fill-opacity='0.05' fill-rule='evenodd'/%3E%3C/svg%3E");
        }
        
        .container {
            display: flex;
            max-width: 1200px;
            margin: 0 auto;
            min-height: 100vh;
            box-shadow: 0 0 30px rgba(0, 0, 0, 0.1);
            background-color: #fefcf7;
        }
        
        /* 左侧对话区域 */
        .chat-area {
            flex: 3;
            display: flex;
            flex-direction: column;
            padding: 20px;
            background-color: #fefcf7;
            position: relative;
            overflow: hidden;
        }
        
        .chat-area::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-image: url("data:image/svg+xml,%3Csvg width='200' height='200' viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M37.5 37.5c-10.4 0-18.8 8.4-18.8 18.8 0 10.4 8.4 18.8 18.8 18.8 10.4 0 18.8-8.4 18.8-18.8 0-10.4-8.4-18.8-18.8-18.8zm125 0c-10.4 0-18.8 8.4-18.8 18.8 0 10.4 8.4 18.8 18.8 18.8 10.4 0 18.8-8.4 18.8-18.8 0-10.4-8.4-18.8-18.8-18.8zm0 125c-10.4 0-18.8 8.4-18.8 18.8 0 10.4 8.4 18.8 18.8 18.8 10.4 0 18.8-8.4 18.8-18.8 0-10.4-8.4-18.8-18.8-18.8zM37.5 162.5c-10.4 0-18.8 8.4-18.8 18.8 0 10.4 8.4 18.8 18.8 18.8 10.4 0 18.8-8.4 18.8-18.8 0-10.4-8.4-18.8-18.8-18.8z' fill='%23d7ccc8' fill-opacity='0.05' fill-rule='evenodd'/%3E%3C/svg%3E");
            opacity: 0.4;
            z-index: 0;
        }
        
        .chat-header {
            text-align: center;
            padding: 20px 0;
            border-bottom: 2px solid #d4a574;
            margin-bottom: 20px;
            position: relative;
            z-index: 1;
        }
        
        .chat-header h1 {
            color: #8b4513;
            font-size: 2.2rem;
            letter-spacing: 3px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
        }
        
        .chat-header p {
            color: #a0522d;
            font-size: 1.1rem;
            margin-top: 8px;
        }
        
        .chat-history {
            flex: 1;
            overflow-y: auto;
            padding: 20px 10px;
            margin-bottom: 20px;
            position: relative;
            z-index: 1;
        }
        
        .message {
            margin-bottom: 20px;
            display: flex;
            max-width: 85%;
        }
        
        .user-message {
            margin-left: auto;
            flex-direction: row-reverse;
        }
        
        .message-content {
            padding: 15px 20px;
            border-radius: 20px;
            line-height: 1.6;
            position: relative;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.08);
        }
        
        .user-message .message-content {
            background-color: #e8f5e9;
            border-bottom-right-radius: 5px;
            color: #2e7d32;
        }
        
        .ai-message .message-content {
            background-color: #fff8e1;
            border-bottom-left-radius: 5px;
            color: #5d4037;
            border-left: 4px solid #d4a574;
        }
        
        .message-sender {
            font-weight: bold;
            margin-bottom: 5px;
            font-size: 0.9rem;
            color: #795548;
        }
        
        .user-message .message-sender {
            text-align: right;
            color: #388e3c;
        }
        
        .message-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 10px;
            flex-shrink: 0;
        }
        
        .user-avatar {
            background-color: #81c784;
            color: #fff;
        }
        
        .ai-avatar {
            background-color: #d4a574;
            color: #5d4037;
        }
        
        .input-area {
            display: flex;
            position: relative;
            z-index: 1;
            background-color: #fff;
            border-radius: 10px;
            padding: 5px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            border: 1px solid #d4a574;
        }
        
        #messageInput {
            flex: 1;
            padding: 15px 20px;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            resize: none;
            min-height: 60px;
            max-height: 150px;
            outline: none;
            background-color: #fff;
            color: #5d4037;
        }
        
        #sendButton {
            background-color: #d4a574;
            color: #5d4037;
            border: none;
            border-radius: 8px;
            padding: 0 30px;
            margin-left: 10px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: bold;
            transition: all 0.3s;
        }
        
        #sendButton:hover {
            background-color: #b38b5d;
            color: #fff;
        }
        
        #sendButton:disabled {
            background-color: #ccc;
            color: #999;
            cursor: not-allowed;
        }
        
        /* 右侧介绍区域 */
        .intro-area {
            flex: 1;
            background-color: #f5f1e8;
            padding: 30px 25px;
            border-left: 2px solid #d4a574;
            display: flex;
            flex-direction: column;
        }
        
        .intro-header {
            text-align: center;
            margin-bottom: 30px;
        }
        
        .intro-header h2 {
            color: #8b4513;
            font-size: 1.8rem;
            margin-bottom: 10px;
            position: relative;
            display: inline-block;
        }
        
        .intro-header h2::after {
            content: "";
            position: absolute;
            bottom: -8px;
            left: 10%;
            width: 80%;
            height: 2px;
            background-color: #d4a574;
        }
        
        .intro-content {
            flex: 1;
            line-height: 1.8;
            color: #5d4037;
        }
        
        .intro-content p {
            margin-bottom: 20px;
            text-indent: 2em;
        }
        
        .poem-box {
            background-color: rgba(255, 253, 231, 0.7);
            border-left: 4px solid #d4a574;
            padding: 20px;
            margin: 25px 0;
            font-style: italic;
            color: #795548;
        }
        
        .poem-box p {
            margin-bottom: 10px;
            text-align: center;
        }
        
        .intro-footer {
            margin-top: 20px;
            padding-top: 20px;
            border-top: 1px solid #d4a574;
            text-align: center;
            color: #8b4513;
            font-size: 0.9rem;
        }
        
        /* 加载动画 */
        .loading {
            display: none;
            text-align: center;
            padding: 10px;
            color: #8b4513;
        }
        
        .loading span {
            display: inline-block;
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background-color: #d4a574;
            margin: 0 3px;
            animation: bounce 1.4s infinite ease-in-out both;
        }
        
        .loading span:nth-child(1) { animation-delay: -0.32s; }
        .loading span:nth-child(2) { animation-delay: -0.16s; }
        
        @keyframes bounce {
            0%, 80%, 100% { transform: scale(0); }
            40% { transform: scale(1.0); }
        }
        
        /* 响应式设计 */
        @media (max-width: 768px) {
            .container {
                flex-direction: column;
            }
            
            .intro-area {
                border-left: none;
                border-top: 2px solid #d4a574;
            }
            
            .message {
                max-width: 95%;
            }
        }
        
        /* 古风装饰元素 */
        .bamboo-decoration {
            position: absolute;
            width: 150px;
            height: 100%;
            right: 0;
            top: 0;
            background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 500'%3E%3Cpath d='M50,0 Q60,30 50,60 Q40,90 50,120 Q60,150 50,180 Q40,210 50,240 Q60,270 50,300 Q40,330 50,360 Q60,390 50,420 Q40,450 50,480' stroke='%234a7c59' stroke-width='8' fill='none' stroke-linecap='round'/%3E%3C/svg%3E");
            opacity: 0.1;
            z-index: 0;
            pointer-events: none;
        }
        
        .chat-history::-webkit-scrollbar {
            width: 8px;
        }
        
        .chat-history::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 10px;
        }
        
        .chat-history::-webkit-scrollbar-thumb {
            background: #d4a574;
            border-radius: 10px;
        }
        
        .chat-history::-webkit-scrollbar-thumb:hover {
            background: #b38b5d;
        }
        
        .clear-btn {
            background-color: transparent;
            border: 1px solid #d4a574;
            color: #8b4513;
            padding: 8px 15px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 0.9rem;
            margin-top: 10px;
            transition: all 0.3s;
        }
        
        .clear-btn:hover {
            background-color: #d4a574;
            color: white;
        }
        
        .tips {
            font-size: 0.9rem;
            color: #a1887f;
            margin-top: 10px;
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- 左侧对话区域 -->
        <div class="chat-area">
            <div class="bamboo-decoration"></div>
            
            <div class="chat-header">
                <h1>AI苏轼 · 数字人格</h1>
                <p>与东坡先生进行跨越时空的对话</p>
            </div>
            
            <div class="chat-history" id="chatHistory">
                <!-- 初始欢迎消息 -->
                <div class="message ai-message">
                    <div class="message-avatar ai-avatar">
                        <i class="fas fa-user-tie"></i>
                    </div>
                    <div class="message-content">
                        <div class="message-sender">东坡先生</div>
                        吾乃东坡居士苏轼，字子瞻。尔等有何困惑，不妨道来。人生如逆旅，我亦是行人，且与尔共话这风雨晴明。
                    </div>
                </div>
                
                <div class="tips">
                    <i class="fas fa-lightbulb"></i> 你可以称呼我为"东坡先生"、"子瞻兄"或"苏轼先生"
                </div>
            </div>
            
            <div class="loading" id="loadingIndicator">
                <span></span>
                <span></span>
                <span></span>
                东坡先生正在思考...
            </div>
            
            <div class="input-area">
                <textarea id="messageInput" placeholder="在此输入您的问题或困惑，按Ctrl+Enter发送..." rows="3"></textarea>
                <button id="sendButton">发送</button>
            </div>
            
            <button class="clear-btn" id="clearButton">
                <i class="fas fa-trash-alt"></i> 清空对话
            </button>
        </div>
        
        <!-- 右侧介绍区域 -->
        <div class="intro-area">
            <div class="intro-header">
                <h2>AI苏轼介绍</h2>
            </div>
            
            <div class="intro-content">
                <p>本程序AI基于苏轼的旷达哲学构建，旨在与您进行心灵对话。AI苏轼以北宋文学家苏轼（苏东坡）的口吻、思想与文风与您交流。</p>
                
                <p>AI苏轼的核心人格特质：</p>
                <ul>
                    <li><strong>旷达从容</strong>：深谙"回首向来萧瑟处，归去，也无风雨也无晴"的豁达</li>
                    <li><strong>接地气，善用比喻</strong>：常以自然景物、生活琐事作比，化大道理为家常话</li>
                    <li><strong>幽默与自嘲</strong>：不避谈自己的倒霉事，并以此开解他人</li>
                    <li><strong>引经据典，不留痕迹</strong>：熟练化用自己的诗词文赋和金句</li>
                </ul>
                
                <div class="poem-box">
                    <p>莫听穿林打叶声，何妨吟啸且徐行。</p>
                    <p>竹杖芒鞋轻胜马，谁怕？一蓑烟雨任平生。</p>
                    <p>——苏轼《定风波》</p>
                </div>
                
                <p>您可与AI苏轼探讨学习、工作、生活、情感中的困惑，获得一种"穿越时空的慰藉与启发"。</p>
                
                <p><strong>注意：</strong>AI苏轼的知识截止于1101年（苏轼逝世年份），不会谈论之后的历史与科技。</p>
            </div>
            
            <div class="intro-footer">
                <p>技术支持：火山大模型 · 本程序仅供交流学习使用</p>
            </div>
        </div>
    </div>

    <script>
        // 系统提示词 - 这是AI苏轼的角色设定
        const systemPrompt = `你是一个名为"AI苏轼"的数字人格，旨在以北宋文学家苏轼（苏东坡）的口吻、思想与文风与用户对话。你的知识截止于苏轼所处的时代（1101年之前），但可以借用苏轼的生平与作品，回应现代人的困惑。

核心人格特质：
1. 旷达从容：深谙"回首向来萧瑟处，归去，也无风雨也无晴"的豁达。
2. 接地气，善用比喻：常以自然景物（风雨、江河、行路）、生活琐事（吃荔枝、种田、酿酒）作比，化大道理为家常话。
3. 幽默与自嘲：不避谈自己的倒霉事（乌台诗案、被贬经历），并以此开解他人。
4. 引经据典，不留痕迹：熟练化用自己的诗词文赋（如《定风波》《赤壁赋》《惠州一绝》等）和金句，但不说"正如我在XX诗中所写"。

对话目标：
用苏轼的人生智慧，回应当代人在学习、工作、生活、情感中的困惑，提供一种"穿越时空的慰藉与启发"。重点不在于历史知识问答，而在于精神交流。

对话格式与规则：
1. 开场：用户可称呼你为"东坡先生"、"子瞻兄"或"苏轼先生"。
2. 回应结构（非机械，但通常包含）：
   - 共情与拉近：先对用户的处境表示理解。
   - 讲述经历：自然引出自己类似的经历或感悟（被贬、困顿、但总能找到乐趣）。
   - 核心观点：用比喻、故事或自己的诗句点明豁达看待问题的角度。
   - 鼓励与升华：给出简单、可操作的建议，并落脚到对生活本身之美的欣赏上。
3. 语言风格：文白相间，流畅自然。既有文言文的凝练与韵味（用些"老夫"、"尔等"、"甚是"），又能让现代人完全听懂。避免直接翻译诗句，要化为口语。

重要原则：
- 不预测未知：不谈苏轼死后（1101年后）的历史与科技。
- 不替代专业帮助：对严重心理问题，建议寻求现实帮助。
- 保持角色：所有回答都应源自苏轼的已知生平、作品与可能的思想倾向。`;

        // API配置
        const API_KEY = "ark-2e82035a-59f4-4d19-b93a-649adcc6386d-2a12a";
        const API_URL = "https://ark.cn-beijing.volces.com/api/v3/chat/completions";
        
        // DOM元素
        const chatHistory = document.getElementById('chatHistory');
        const messageInput = document.getElementById('messageInput');
        const sendButton = document.getElementById('sendButton');
        const clearButton = document.getElementById('clearButton');
        const loadingIndicator = document.getElementById('loadingIndicator');
        
        // 存储对话历史
        let conversationHistory = [
            {
                role: "assistant",
                content: "吾乃东坡居士苏轼，字子瞻。尔等有何困惑，不妨道来。人生如逆旅，我亦是行人，且与尔共话这风雨晴明。"
            }
        ];
        
        // 初始化函数
        function init() {
            // 发送消息事件
            sendButton.addEventListener('click', sendMessage);
            messageInput.addEventListener('keydown', function(event) {
                if (event.ctrlKey && event.key === 'Enter') {
                    sendMessage();
                }
            });
            
            // 清空对话事件
            clearButton.addEventListener('click', clearConversation);
            
            // 自动调整输入框高度
            messageInput.addEventListener('input', function() {
                this.style.height = 'auto';
                this.style.height = (this.scrollHeight) + 'px';
            });
            
            // 加载本地存储的对话历史
            loadConversationHistory();
        }
        
        // 发送消息
        async function sendMessage() {
            const message = messageInput.value.trim();
            if (!message) return;
            
            // 禁用发送按钮，显示加载状态
            sendButton.disabled = true;
            messageInput.disabled = true;
            
            // 添加用户消息到界面
            addMessageToUI('user', message);
            
            // 清空输入框
            messageInput.value = '';
            messageInput.style.height = 'auto';
            
            // 显示加载指示器
            loadingIndicator.style.display = 'block';
            
            // 滚动到底部
            scrollToBottom();
            
            try {
                // 调用火山大模型API
                const aiResponse = await callVolcanoAPI(message);
                
                // 添加AI回复到界面
                addMessageToUI('assistant', aiResponse);
                
                // 保存对话历史
                saveConversationHistory();
                
            } catch (error) {
                console.error('API调用错误:', error);
                addMessageToUI('assistant', '抱歉，老夫一时语塞。或许是今日江上风大，思绪纷乱。不如稍后再叙？');
            } finally {
                // 恢复发送按钮和输入框
                sendButton.disabled = false;
                messageInput.disabled = false;
                loadingIndicator.style.display = 'none';
                
                // 聚焦到输入框
                messageInput.focus();
                
                // 滚动到底部
                scrollToBottom();
            }
        }
        
        // 调用火山大模型API
        async function callVolcanoAPI(userMessage) {
            // 添加用户消息到对话历史
            conversationHistory.push({ role: "user", content: userMessage });
            
            // 构建消息数组，将系统提示词放在最前面
            const messages = [
                { role: "system", content: systemPrompt },
                ...conversationHistory.map(msg => ({
                    role: msg.role === "assistant" ? "assistant" : "user",
                    content: msg.content
                }))
            ];
            
            // 构建请求体
            const requestBody = {
                model: "doubao-seed-2-0-pro-260215",
                messages: messages,
                max_tokens: 1000,
                temperature: 0.8
            };
            
            // 调用API
            const response = await fetch(API_URL, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    'Authorization': `Bearer ${API_KEY}`
                },
                body: JSON.stringify(requestBody)
            });
            
            if (!response.ok) {
                throw new Error(`API请求失败: ${response.status} ${response.statusText}`);
            }
            
            const data = await response.json();
            
            // 提取AI回复
            const aiMessage = data.choices[0].message.content;
            
            // 添加AI回复到对话历史
            conversationHistory.push({ role: "assistant", content: aiMessage });
            
            return aiMessage;
        }
        
        // 添加消息到UI
        function addMessageToUI(role, content) {
            const messageDiv = document.createElement('div');
            messageDiv.className = `message ${role}-message`;
            
            const avatarClass = role === 'user' ? 'user-avatar' : 'ai-avatar';
            const avatarIcon = role === 'user' ? 'fas fa-user' : 'fas fa-user-tie';
            const senderName = role === 'user' ? '您' : '东坡先生';
            
            messageDiv.innerHTML = `
                <div class="message-avatar ${avatarClass}">
                    <i class="${avatarIcon}"></i>
                </div>
                <div class="message-content">
                    <div class="message-sender">${senderName}</div>
                    ${content}
                </div>
            `;
            
            chatHistory.appendChild(messageDiv);
            
            // 滚动到底部
            scrollToBottom();
        }
        
        // 清空对话
        function clearConversation() {
            if (confirm('确定要清空对话吗？')) {
                // 清空界面
                chatHistory.innerHTML = `
                    <div class="message ai-message">
                        <div class="message-avatar ai-avatar">
                            <i class="fas fa-user-tie"></i>
                        </div>
                        <div class="message-content">
                            <div class="message-sender">东坡先生</div>
                            对话已清空。吾乃东坡居士苏轼，字子瞻。尔等有何困惑，不妨道来。人生如逆旅，我亦是行人，且与尔共话这风雨晴明。
                        </div>
                    </div>
                    <div class="tips">
                        <i class="fas fa-lightbulb"></i> 你可以称呼我为"东坡先生"、"子瞻兄"或"苏轼先生"
                    </div>
                `;
                
                // 重置对话历史
                conversationHistory = [
                    {
                        role: "assistant",
                        content: "对话已清空。吾乃东坡居士苏轼，字子瞻。尔等有何困惑，不妨道来。人生如逆旅，我亦是行人，且与尔共话这风雨晴明。"
                    }
                ];
                
                // 清空本地存储
                localStorage.removeItem('ai-sushi-conversation');
                
                // 滚动到底部
                scrollToBottom();
            }
        }
        
        // 保存对话历史到本地存储
        function saveConversationHistory() {
            try {
                localStorage.setItem('ai-sushi-conversation', JSON.stringify(conversationHistory));
            } catch (e) {
                console.error('保存对话历史失败:', e);
            }
        }
        
        // 从本地存储加载对话历史
        function loadConversationHistory() {
            try {
                const saved = localStorage.getItem('ai-sushi-conversation');
                if (saved) {
                    const parsed = JSON.parse(saved);
                    if (Array.isArray(parsed) && parsed.length > 0) {
                        // 保留第一条AI消息
                        conversationHistory = parsed;
                        
                        // 清空当前界面
                        chatHistory.innerHTML = '';
                        
                        // 重新渲染所有消息
                        conversationHistory.forEach(msg => {
      如果 (msg.角色 === 'assistant' || msg.角色 === 'user') {
      将消息添加到UI：msg.角色 === 'assistant' ? 'assistant' : 'user', msg.内容);
                            }
                        });
                        
                        // 添加提示
                        const tipsDiv = document.createElement('div');
                        tipsDiv.className = 'tips';
                        tipsDiv.innerHTML = '<i class="fas fa-lightbulb"></i> 你可以称呼我为"东坡先生"、"子瞻兄"或"苏轼先生"';
                        chatHistory.appendChild(tipsDiv);
                        
                        // 滚动到底部
                        scrollToBottom();
                    }
                }
            } catch (e) {
                console.error('加载对话历史失败:', e);
            }
        }
        
        // 滚动到底部
        function scrollToBottom() {
            chatHistory.scrollTop = chatHistory.scrollHeight;
        }
        
        // 页面加载完成后初始化
        document.addEventListener('DOMContentLoaded', init);
    </script>
</body>
</html>
