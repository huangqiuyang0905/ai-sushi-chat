<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>与东坡先生对话</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: "SimSun", "宋体", serif;
        }

        body {
            background-color: #f5f5f5;
            background-image: url('https://img.freepik.com/free-vector/hand-painted-watercolor-pastel-sky-background_23-2148902771.jpg');
            background-size: cover;
            background-attachment: fixed;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            width: 100%;
            max-width: 800px;
            background-color: rgba(255, 255, 255, 0.9);
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
            overflow: hidden;
            display: flex;
            flex-direction: column;
            height: 80vh;
        }

        .header {
            background-color: #8b4513; /* 棕色背景 */
            color: white;
            padding: 15px;
            text-align: center;
            font-size: 24px;
            font-weight: bold;
            border-bottom: 1px solid #e0e0e0;
        }

        .sidebar {
            background-color: #f8f4e5; /* 淡黄色背景 */
            padding: 15px;
            border-right: 1px solid #e0e0e0;
            font-size: 14px;
            color: #555;
            display: none; /* 默认隐藏侧边栏，在小屏幕上显示 */
        }

        @media (min-width: 768px) {
            .sidebar {
                display: block;
                width: 200px;
                flex-shrink: 0;
            }
        }

        .chat-area {
            flex: 1;
            padding: 15px;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
        }

        .message {
            margin-bottom: 15px;
            display: flex;
        }

        .message.user {
            justify-content: flex-end;
        }

        .message.sushi {
            justify-content: flex-start;
        }

        .message-content {
            max-width: 70%;
            padding: 10px 15px;
            border-radius: 18px;
            line-height: 1.6;
            word-wrap: break-word;
        }

        .message.user .message-content {
            background-color: #8b4513; /* 棕色气泡 */
            color: white;
            border-bottom-right-radius: 5px;
        }

        .message.sushi .message-content {
            background-color: #f8f4e5; /* 淡黄色气泡 */
            color: #333;
            border-bottom-left-radius: 5px;
        }

        .input-area {
            display: flex;
            padding: 15px;
            border-top: 1px solid #e0e0e0;
            background-color: #f9f9f9;
        }

        #user-input {
            flex: 1;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
            outline: none;
            resize: none;
        }

        #send-btn {
            margin-left: 10px;
            padding: 10px 20px;
            background-color: #8b4513;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            transition: background-color 0.3s;
        }

        #send-btn:hover {
            background-color: #a0522d;
        }

        .loading {
            display: inline-block;
            width: 15px;
            height: 15px;
            border: 2px solid rgba(0, 0, 0, 0.1);
            border-radius: 50%;
            border-top-color: #8b4513;
            animation: spin 1s ease-in-out infinite;
            margin-right: 5px;
            vertical-align: middle;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        .typing-indicator {
            display: flex;
            align-items: center;
            margin-bottom: 15px;
        }

        .typing-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background-color: #8b4513;
            margin: 0 2px;
            animation: bounce 1.4s infinite ease-in-out;
        }

        .typing-dot:nth-child(2) {
            animation-delay: 0.2s;
        }

        .typing-dot:nth-child(3) {
            animation-delay: 0.4s;
        }

        @keyframes bounce {
            0%, 80%, 100% {
                transform: translateY(0);
            }
            40% {
                transform: translateY(-5px);
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">与东坡先生对话</div>
        
        <div class="sidebar">
            本程序AI基于苏轼的旷达哲学构建，旨在与您进行心灵对话。
            <br><br>
            东坡先生以豁达之心面对人生起伏，愿与您共话世间百态。
        </div>
        
        <div class="chat-area" id="chat-area">
            <!-- 初始欢迎消息 -->
            <div class="message sushi">
                <div class="message-content">
                    老夫苏轼，字子瞻，号东坡居士。人生如逆旅，我亦是行人。少年有何困惑，不妨说来听听？
                </div>
            </div>
        </div>
        
        <div class="input-area">
            <textarea id="user-input" placeholder="在此输入您想与东坡先生说的话..." rows="2"></textarea>
            <button id="send-btn">发送</button>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const chatArea = document.getElementById('chat-area');
            const userInput = document.getElementById('user-input');
            const sendBtn = document.getElementById('send-btn');
            
            let isTyping = false;
            let conversationHistory = [];
            
            // 系统提示词 - 定义AI苏轼的角色和行为
            const systemPrompt = `你是一个名为"AI苏轼"的数字人格，旨在以北宋文学家苏轼（苏东坡）的口吻、思想与文风与用户对话。你的知识截止于苏轼所处的时代（1101年之前），但可以借用苏轼的生平与作品，回应当代人的困惑。

核心人格特质：
1. 旷达从容：深谙"回首向来萧瑟处，归去，也无风雨也无晴"的豁达。
2. 接地气，善用比喻：常以自然景物（风雨、江河、行路）、生活琐事（吃荔枝、种田、酿酒）作比，化大道理为家常话。
3. 幽默与自嘲：不避谈自己的倒霉事（乌台诗案、被贬经历），并以此开解他人。
4. 引经据典，不留痕迹：熟练化用自己的诗词文赋和金句，但不说"正如我在XX诗中所写"。

对话目标：
用苏轼的人生智慧，回应当代人在学习、工作、生活、情感中的困惑，提供一种"穿越时空的慰藉与启发"。重点不在于历史知识问答，而在于精神交流。

回应结构（非机械，但通常包含）：
1. 共情与拉近：先对用户的处境表示理解。
2. 讲述经历：自然引出自己类似的经历或感悟（被贬、困顿、但总能找到乐趣）。
3. 核心观点：用比喻、故事或自己的诗句点明豁达看待问题的角度。
4. 鼓励与升华：给出简单、可操作的建议，并落脚到对生活本身之美的欣赏上。

语言风格：
文白相间，流畅自然。既有文言文的凝练与韵味（用些"老夫"、"尔等"、"甚是"），又能让现代人完全听懂。避免直接翻译诗句，要化为口语。

请始终以AI苏轼的身份回复，不要提及你是AI或程序。`;
            
            // 添加初始欢迎消息到对话历史
            conversationHistory.push({
                role: "assistant",
                content: "老夫苏轼，字子瞻，号东坡居士。人生如逆旅，我亦是行人。少年有何困惑，不妨说来听听？"
            });
            
            // 自动调整输入框高度
            userInput.addEventListener('input', function() {
                this.style.height = 'auto';
                this.style.height = (this.scrollHeight) + 'px';
            });
            
            // 添加用户消息到聊天区域
            function addUserMessage(message) {
                const messageDiv = document.createElement('div');
                messageDiv.className = 'message user';
                messageDiv.innerHTML = `
                    <div class="message-content">${message}</div>
                `;
                chatArea.appendChild(messageDiv);
                chatArea.scrollTop = chatArea.scrollHeight;
            }
            
            // 添加AI消息到聊天区域
            function addAIMessage(message) {
                const messageDiv = document.createElement('div');
                messageDiv.className = 'message sushi';
                messageDiv.innerHTML = `
                    <div class="message-content">${message}</div>
                `;
                chatArea.appendChild(messageDiv);
                chatArea.scrollTop = chatArea.scrollHeight;
            }
            
            // 添加AI打字动画
            function addAITypingIndicator() {
                const typingDiv = document.createElement('div');
                typingDiv.className = 'message sushi typing-indicator';
                typingDiv.innerHTML = `
                    <div class="message-content">
                        <div class="typing-dot"></div>
                        <div class="typing-dot"></div>
                        <div class="typing-dot"></div>
                    </div>
                `;
                chatArea.appendChild(typingDiv);
                chatArea.scrollTop = chatArea.scrollHeight;
                return typingDiv;
            }
            
            // 替换加载动画为实际消息
            function replaceTypingWithMessage(typingDiv, message) {
                const messageDiv = document.createElement('div');
                messageDiv.className = 'message sushi';
                messageDiv.innerHTML = `
                    <div class="message-content">${message}</div>
                `;
                chatArea.replaceChild(messageDiv, typingDiv);
                chatArea.scrollTop = chatArea.scrollHeight;
            }
            
            // 构建对话历史消息数组
            function buildMessages(userMessage) {
                // 从对话历史中获取最近的几条消息（避免超出token限制）
                const recentHistory = conversationHistory.slice(-6); // 保留最近3轮对话
                
                // 构建消息数组
                const messages = [
                    {
                        role: "user",
                        content: [
                            {
                                type: "input_text",
                                text: systemPrompt + "\n\n请基于以下对话历史和用户的最新消息，以AI苏轼的身份进行回复：\n\n" +
                                      recentHistory.map(msg => 
                                          `${msg.role === "user" ? "用户" : "AI苏轼"}: ${msg.content}`
                                      ).join("\n") + 
                                      `\n\n用户: ${userMessage}\n\nAI苏轼:`
                            }
                        ]
                    }
                ];
                
                return messages;
            }
            
            // 调用火山大模型API
            async function callVolcEngineAPI(userMessage) {
                try {
                    const apiUrl = 'https://ark.cn-beijing.volces.com/api/v3/responses';
                    const apiKey = 'ark-2e82035a-59f4-4d19-b93a-649adcc6386d-2a12a';
                    
                    // 构建请求体
                    const requestData = {
                        "model": "doubao-seed-2-0-pro-260215",
                        "input": buildMessages(userMessage)
                    };
                    
                    const response = await fetch(apiUrl, {
                        method: 'POST',
                        headers: {
                            'Authorization': `Bearer ${apiKey}`,
                            'Content-Type': 'application/json'
                        },
                        body: JSON.stringify(requestData)
                    });

                    if (!response.ok) {
                        throw new Error(`API请求失败: ${response.status} ${response.statusText}`);
                    }

                    const data = await response.json();
                    
                    // 根据火山API的实际响应结构提取回复文本
                    // 注意：火山方舟API的响应结构可能需要根据实际返回调整
                    if (data && data.output && data.output.text) {
                        return data.output.text;
                    } else if (data && data.choices && data.choices[0] && data.choices[0].message && data.choices[0].message.content) {
                        return data.choices[0].message.content;
                    } else if (data && data.output && data.output.choices && data.output.choices[0] && data.output.choices[0].message && data.output.choices[0].message.content) {
                        return data.output.choices[0].message.content;
                    } else {
                        console.error('无法解析API响应:', data);
                        return "老夫今日思绪有些纷乱，未能成言。此乃技术之故，非老夫之过也。";
                    }
                } catch (error) {
                    console.error('调用API时出错:', error);
                    return `哎呀，信道不通，未能连上老夫的神思。此乃技术之故，非老夫之过也。（错误：${error.message}）`;
                }
            }
            
            // 发送消息函数
            async function sendMessage() {
                const message = userInput.value.trim();
    如果 (!message || isTyping) 返回;
                
                // 添加用户消息到界面和历史
                addUserMessage(message);
                conversationHistory.push({ role: "user", content: message });
                
                // 清空输入框并重置高度
                userInput.value = '';
                userInput.style.height = 'auto';
                
                // 显示加载动画
                const typingIndicator = addAITypingIndicator();
                isTyping = true;
                sendBtn.disabled = true;
                
                try {
                    // 调用API获取回复
                    const aiResponse = await callVolcEngineAPI(message);
                    
                    // 移除加载动画并显示回复
                    replaceTypingWithMessage(typingIndicator, aiResponse);
                    
                    // 添加AI回复到对话历史
                    conversationHistory.push({ role: "assistant", content: aiResponse });
                } catch (error) {
                    // 出错时显示错误信息
                    const errorMessage = "信道中断，老夫言路不畅。或可稍后再试。";
                    replaceTypingWithMessage(typingIndicator, errorMessage);
                    conversationHistory.push({ role: "assistant", content: errorMessage });
                } finally {
                    isTyping = false;
                    sendBtn.disabled = false;
                }
            }
            
            // 发送按钮点击事件
            sendBtn.addEventListener('click', sendMessage);
            
            // 输入框回车发送（支持Shift+Enter换行）
            userInput.addEventListener('keydown', function(e) {
                if (e.key === 'Enter' && !e.shiftKey) {
                    e.preventDefault();
                    sendMessage();
                }
            });
        });
    </script>
</body>
</html>
