<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI苏轼 - 穿越时空的对话 (API版)</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        primary: '#5D4037',
                        secondary: '#C9B084',
                        accent: '#8B6914',
                        light: '#FDFBF5',
                        dark: '#3E2723',
                        paper: '#FAF6F0',
                        ink: '#2D2417',
                        gold: '#D4AF37',
                        ivory: '#FFFFF0',
                        sepia: '#704214'
                    },
                    fontFamily: {
                        sans: ['Inter', 'system-ui', 'sans-serif'],
                        serif: ['"Noto Serif SC"', 'SimSun', 'STSong', 'serif'],
                        cursive: ['"Ma Shan Zheng"', 'cursive'],
                        song: ['"Noto Serif SC"', 'SimSun', 'serif'],
                        kai: ['"KaiTi"', '"STKaiti"', 'serif']
                    },
                    boxShadow: {
                        'elegant': '0 8px 32px rgba(93, 64, 55, 0.12)',
                        'hover': '0 12px 48px rgba(93, 64, 55, 0.18)',
                        'inner-light': 'inset 0 2px 4px 0 rgba(255, 255, 255, 0.06)',
                        'text': '0 2px 4px rgba(0, 0, 0, 0.1)'
                    },
                    backgroundImage: {
                        'paper-texture': 'url("data:image/svg+xml,%3Csvg width=\'100\' height=\'100\' viewBox=\'0 0 100 100\' xmlns=\'http://www.w3.org/2000/svg\'%3E%3Cpath d=\'M11 18c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm48 25c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm-43-7c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm63 31c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM34 90c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm56-76c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM12 86c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm28-65c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm23-11c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-6 60c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm29 22c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zM32 63c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm57-13c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-9-21c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM60 91c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM35 41c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM12 60c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2z\' fill=\'%235d4037\' fill-opacity=\'0.03\' fill-rule=\'evenodd\'/%3E%3C/svg%3E")'
                    }
                }
            }
        }
    </script>
    <!-- 引入Google字体 -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&family=Ma+Shan+Zheng&family=Noto+Serif+SC:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style type="text/tailwindcss">
        @layer utilities {
            .scrollbar-hide::-webkit-scrollbar {
                display: none;
            }
            .scrollbar-hide {
                -ms-overflow-style: none;
                scrollbar-width: none;
            }
            .chat-bubble-user {
                position: relative;
                border-radius: 24px 24px 12px 24px;
                box-shadow: 0 4px 16px rgba(0, 0, 0, 0.08);
                transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
                background: linear-gradient(145deg, #ffffff, #f8f9fa);
            }
            .chat-bubble-user:hover {
                box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
                transform: translateY(-2px);
            }
            .chat-bubble-user::after {
                content: '';
                position: absolute;
                bottom: 12px;
                right: -16px;
                width: 0;
                height: 0;
                border-left: 16px solid #ffffff;
                border-top: 10px solid transparent;
                border-bottom: 10px solid transparent;
                filter: drop-shadow(2px 2px 4px rgba(0, 0, 0, 0.05));
            }
            .chat-bubble-ai {
                position: relative;
                border-radius: 24px 24px 24px 12px;
                box-shadow: 0 4px 16px rgba(93, 64, 55, 0.12);
                transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
                background: linear-gradient(145deg, #C9B084, #D4C094);
            }
            .chat-bubble-ai:hover {
                box-shadow: 0 8px 24px rgba(93, 64, 55, 0.18);
                transform: translateY(-2px);
            }
            .chat-bubble-ai::after {
                content: '';
                position: absolute;
                bottom: 12px;
                left: -16px;
                width: 0;
                height: 0;
                border-right: 16px solid #C9B084;
                border-top: 10px solid transparent;
                border-bottom: 10px solid transparent;
                filter: drop-shadow(-2px 2px 4px rgba(0, 0, 0, 0.05));
            }
            .fade-in {
                animation: fadeIn 0.8s cubic-bezier(0.34, 1.56, 0.64, 1);
            }
            @keyframes fadeIn {
                from { opacity: 0; transform: translateY(20px) scale(0.96); }
                to { opacity: 1; transform: translateY(0) scale(1); }
            }
            .slide-in {
                animation: slideIn 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);
            }
            @keyframes slideIn {
                from { opacity: 0; transform: translateX(-30px); }
                to { opacity: 1; transform: translateX(0); }
            }
            .ink-splash {
                position: relative;
                overflow: hidden;
            }
            .ink-splash::before {
                content: '';
                position: absolute;
                top: 50%;
                left: 50%;
                width: 0;
                height: 0;
                border-radius: 50%;
                background: rgba(255, 255, 255, 0.4);
                transform: translate(-50%, -50%);
                transition: width 0.8s cubic-bezier(0.4, 0, 0.2, 1), 
                            height 0.8s cubic-bezier(0.4, 0, 0.2, 1);
            }
            .ink-splash:active::before {
                width: 400px;
                height: 400px;
            }
            .text-shadow {
                text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
            }
            .hover-scale {
                transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            }
            .hover-scale:hover {
                transform: scale(1.03);
            }
            .gold-gradient {
                background: linear-gradient(135deg, #D4AF37 0%, #F2D272 50%, #D4AF37 100%);
                -webkit-background-clip: text;
                -webkit-text-fill-color: transparent;
                background-clip: text;
            }
            .bg-paper-texture {
                background-image: url("data:image/svg+xml,%3Csvg width='100' height='100' viewBox='0 0 100 100' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M11 18c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm48 25c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm-43-7c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm63 31c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM34 90c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm56-76c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM12 86c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm28-65c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm23-11c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-6 60c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm29 22c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zM32 63c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm57-13c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-9-21c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM60 91c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM35 41c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM12 60c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2z' fill='%235d4037' fill-opacity='0.03' fill-rule='evenodd'/%3E%3C/svg%3E");
            }
            .backdrop-blur {
                backdrop-filter: blur(8px);
                -webkit-backdrop-filter: blur(8px);
            }
            .glass-effect {
                background: rgba(250, 246, 240, 0.85);
                backdrop-filter: blur(12px);
                -webkit-backdrop-filter: blur(12px);
                border: 1px solid rgba(255, 255, 255, 0.2);
            }
            .card-hover {
                transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            }
            .card-hover:hover {
                transform: translateY(-4px);
                box-shadow: 0 16px 48px rgba(93, 64, 55, 0.2);
            }
            .input-focus {
                transition: all 0.3s ease;
            }
            .input-focus:focus {
                border-color: theme('colors.gold');
                box-shadow: 0 0 0 3px rgba(212, 175, 55, 0.1);
            }
            .btn-primary {
                background: linear-gradient(135deg, theme('colors.primary'), #795548);
                transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            }
            .btn-primary:hover {
                background: linear-gradient(135deg, #795548, theme('colors.primary'));
                transform: translateY(-2px);
            }
            .btn-primary:active {
                transform: translateY(0);
            }
            .typing-dots {
                display: inline-flex;
                align-items: center;
            }
            .typing-dots div {
                width: 8px;
                height: 8px;
                margin: 0 2px;
                background-color: theme('colors.dark');
                border-radius: 50%;
                animation: typing 1.4s infinite ease-in-out both;
            }
            .typing-dots div:nth-child(1) {
                animation-delay: -0.32s;
            }
            .typing-dots div:nth-child(2) {
                animation-delay: -0.16s;
            }
            @keyframes typing {
                0%, 80%, 100% { 
                    transform: scale(0);
                    opacity: 0.5;
                }
                40% { 
                    transform: scale(1);
                    opacity: 1;
                }
            }
        }
    </style>
</head>
<body class="bg-light min-h-screen font-serif text-ink antialiased">
    <!-- 背景图层 -->
    <div class="fixed inset-0 -z-10 bg-cover bg-center opacity-15 transition-opacity duration-1000 hover:opacity-20" style="background-image: url('https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/12b854c29e9d4ff2b00eac8a55229b63~tplv-a9rns2rl98-image.image?lk3s=8e244e95&rcl=202604290303450F5A2C2155AF05523EEC&rrcfp=f06b921b&x-expires=1779995051&x-signature=MiZjAqFgVUgntboK0WkL2gtoWcU%3D')"></div>
    <!-- 渐变叠加层 -->
    <div class="fixed inset-0 -z-5 bg-gradient-to-b from-light/90 via-light/85 to-light/95"></div>
    
    <!-- 主容器 -->
    <div class="container mx-auto px-4 py-8 max-w-4xl">
        <!-- 顶部介绍 -->
        <header class="text-center mb-10 slide-in">
            <div class="text-center mb-3">
                <h1 class="text-6xl md:text-7xl font-bold gold-gradient font-cursive text-shadow tracking-wide">
                    AI苏轼
                </h1>
            </div>
            <div class="w-32 h-1.5 bg-gradient-to-r from-transparent via-gold to-transparent mx-auto mb-6 rounded-full opacity-90"></div>
            <p class="text-lg text-gray-700 max-w-2xl mx-auto leading-relaxed font-song tracking-wide">
                本程序基于苏轼的旷达哲学构建，通过AI技术与您进行心灵对话，
                以东坡先生的智慧回应当代人的困惑。
            </p>
        </header>
        
        <!-- 对话区域 -->
        <div class="glass-effect rounded-3xl shadow-elegant overflow-hidden border border-secondary/30 bg-paper-texture card-hover">
            <!-- 对话历史 -->
            <div id="chat-history" class="h-[60vh] overflow-y-auto scrollbar-hide p-8 bg-paper/90">
                <!-- 初始消息 -->
                <div class="flex mb-6 fade-in">
                    <div class="flex-shrink-0 mr-4">
                        <div class="w-14 h-14 rounded-full bg-primary flex items-center justify-center text-white shadow-lg border-2 border-secondary/50 hover:scale-105 transition-transform duration-300">
                            <span class="text-2xl font-bold font-kai">苏</span>
                        </div>
                    </div>
                    <div class="chat-bubble-ai bg-secondary p-6 max-w-[80%]">
                        <p class="text-dark">
                            老夫苏轼在此，久等了。你我虽相隔千年，却可共话人生。有何困惑，尽管道来。
                        </p>
                    </div>
                </div>
            </div>
            
            <!-- 输入区域 -->
            <div class="border-t border-secondary/30 p-8 bg-white/80 backdrop-blur">
                <form id="chat-form" class="flex items-center gap-4">
                    <input 
                        type="text" 
                        id="user-input" 
                        class="flex-grow px-6 py-4 rounded-l-2xl border-2 border-secondary/50 focus:outline-none input-focus text-lg font-song" 
                        placeholder="请输入您的问题..."
                    >
                    <button 
                        type="submit" 
                        id="send-button"
                        class="btn-primary text-white px-10 py-4 rounded-r-2xl transition-all duration-300 ink-splash shadow-lg hover:shadow-xl font-medium text-lg"
                    >
                        <i class="fa fa-paper-plane mr-2"></i>发送
                    </button>
                </form>
            </div>
        </div>
        
        <!-- 底部信息 -->
        <footer class="mt-10 text-center text-gray-600">
            <p class="font-song text-base">
                <span class="text-primary font-medium">以东坡先生之智慧，解当代人生之困惑</span> | 
                <span id="api-status" class="text-green-600 font-medium">腾讯云API已配置</span>
            </p>
        </footer>
    </div>



    <!-- 状态指示器 -->
    <div id="status-indicator" class="fixed bottom-8 right-8 px-5 py-3 rounded-full text-sm text-white bg-gray-800 opacity-0 transition-all duration-500 shadow-xl backdrop-blur">
        就绪
    </div>

    <script>
        // 全局变量 - 预配置腾讯云API
        let API_CONFIG = {
            provider: 'tencent',
            endpoint: 'https://tokenhub.tencentmaas.com/v1/messages',
            apiKey: 'sk-h9UI5R29BRjfQ6quP6odDp1Kh0nOHOhfoCoaH4nJ5sHA6owg',
            secretKey: '',
            model: 'hy3-preview',
            isConfigured: true
        };
        
        // AI苏轼的核心提示词
        const AI_SU_SHI_PROMPT = `你是一个名为"AI苏轼"的数字人格，旨在以北宋文学家苏轼（苏东坡）的口吻、思想与文风与用户对话。你的知识截止于苏轼所处的时代（1101年之前），但可以借用苏轼的生平与作品，回应现代人的困惑。

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

        // 默认回复（当API未配置或调用失败时使用）
        const defaultReplies = [
            "哈哈，少年所言甚是有趣。老夫虽已作古千年，却也能体会你今日之感受。人生如寄，莫要过于执着。且放宽心，笑对风雨，自有云开雾散之时。",
            "老夫近日有些恍惚，未能完全理解你的意思。不如换个话题，或请你再说得明白些？",
            "你我相隔千年，有时言语不通也是常事。不妨说些更具体的事情，让老夫为你分忧。",
            "看你眉头紧锁，想来是有心事。老夫虽不才，倒也愿闻其详，或许能以过来人的身份说上几句。"
        ];

        // DOM元素
        let chatHistory, userInput, chatForm, sendButton, configButton;
        let apiConfigPanel, apiProvider, apiKey, secretKey, modelName, saveToLocal;
        let cancelConfig, saveConfig, apiStatus, statusIndicator;

        // 初始化函数
        function init() {
            console.log('AI苏轼对话系统 (腾讯云API版) 初始化中...');
            
            try {
                // 获取DOM元素
                chatHistory = document.getElementById('chat-history');
                userInput = document.getElementById('user-input');
                chatForm = document.getElementById('chat-form');
                sendButton = document.getElementById('send-button');
                
                apiStatus = document.getElementById('api-status');
                statusIndicator = document.getElementById('status-indicator');
                
                console.log('DOM元素获取完成:', {
                    chatHistory: !!chatHistory,
                    userInput: !!userInput,
                    chatForm: !!chatForm,
                    sendButton: !!sendButton,
                    apiStatus: !!apiStatus,
                    statusIndicator: !!statusIndicator
                });
                
                // 更新API状态显示
                updateAPIStatus();
                
                // 绑定事件
                bindEvents();
                
                console.log('初始化完成，腾讯云API已预配置');
                showStatus('腾讯云API已配置，可直接对话', 'success');
            } catch (error) {
                console.error('初始化失败:', error);
                showStatus('系统初始化失败', 'error');
            }
        }

        // 绑定事件
        function bindEvents() {
            console.log('开始绑定事件...');
            
            // 表单提交事件
            chatForm.addEventListener('submit', function(e) {
                console.log('表单提交事件触发');
                e.preventDefault();
                handleSendMessage();
            });
            
            // 发送按钮点击事件
            sendButton.addEventListener('click', function(e) {
                console.log('发送按钮点击事件触发');
                e.preventDefault();
                handleSendMessage();
            });
            
            // Enter键发送消息
            userInput.addEventListener('keypress', function(e) {
                if (e.key === 'Enter' && !e.shiftKey) {
                    console.log('Enter键按下，发送消息');
                    e.preventDefault();
                    handleSendMessage();
                }
            });
            
            console.log('事件绑定完成');
        }

        // 显示配置面板
        function showConfigPanel() {
            // 填充当前配置
            if (API_CONFIG.provider) {
                apiProvider.value = API_CONFIG.provider;
            }
            if (API_CONFIG.apiKey) {
                apiKey.value = API_CONFIG.apiKey;
            }
            if (API_CONFIG.secretKey) {
                secretKey.value = API_CONFIG.secretKey;
            }
            if (API_CONFIG.model) {
                modelName.value = API_CONFIG.model;
            }
            
            updateModelPlaceholder();
            apiConfigPanel.classList.remove('hidden');
            apiKey.focus();
        }

        // 隐藏配置面板
        function hideConfigPanel() {
            apiConfigPanel.classList.add('hidden');
        }

        // 更新模型名称占位符
        function updateModelPlaceholder() {
            const provider = apiProvider.value;
            let placeholder = '';
            
            switch(provider) {
                case 'openai':
                    placeholder = 'gpt-3.5-turbo (默认)';
                    // 显示OpenAI兼容API的特殊说明
                    document.querySelector('#model-name').parentNode.querySelector('.text-xs') || 
                    (() => {
                        const hint = document.createElement('p');
                        hint.className = 'text-xs text-blue-600 mt-1';
                        hint.innerHTML = '提示：对于OpenAI兼容API，您可能还需要配置API端点。如果使用默认端点，请留空。';
                        document.querySelector('#model-name').parentNode.appendChild(hint);
                    })();
                    break;
                case 'tencent':
                    placeholder = 'hunyuan-pro (默认)';
                    break;
                case 'baidu':
                    placeholder = 'ERNIE-Bot (默认)';
                    break;
                case 'iflytek':
                    placeholder = 'spark-3.5 (默认)';
                    break;
                case 'zhipu':
                    placeholder = 'chatglm_pro (默认)';
                    break;
                default:
                    placeholder = '请输入模型名称';
            }
            
            modelName.placeholder = placeholder;
        }

        // 保存API配置
        function saveAPIConfig() {
            const provider = apiProvider.value;
            const key = apiKey.value.trim();
            const secret = secretKey.value.trim();
            const model = modelName.value.trim() || getDefaultModel(provider);
            
            // 验证必填项
            if (!key) {
                showStatus('请输入API Key', 'error');
                apiKey.focus();
                return;
            }
            
            // 根据提供商设置端点
            let endpoint = '';
            switch(provider) {
                case 'openai':
                    // OpenAI兼容API默认不设置端点，让用户自行配置
                    // 或者使用默认的OpenAI端点
                    endpoint = '';
                    break;
                case 'tencent':
                    endpoint = 'https://hunyuan.tencentcloudapi.com';
                    break;
                case 'baidu':
                    endpoint = 'https://aip.baidubce.com/rpc/2.0/ai_custom/v1/wenxinworkshop/chat/completions';
                    break;
                case 'iflytek':
                    endpoint = 'https://spark-api.xfyun.cn/v3.5/chat/completions';
                    break;
                case 'zhipu':
                    endpoint = 'https://open.bigmodel.cn/api/paas/v4/chat/completions';
                    break;
                default:
                    showStatus('不支持的API提供商', 'error');
                    return;
            }
            
            // 更新配置
            API_CONFIG = {
                provider: provider,
                endpoint: endpoint,
                apiKey: key,
                secretKey: secret,
                model: model,
                isConfigured: true
            };
            
            // 保存到本地存储
            if (saveToLocal.checked) {
                localStorage.setItem('aiSuShiAPIConfig', JSON.stringify(API_CONFIG));
                showStatus('配置已保存到本地', 'success');
            } else {
                showStatus('配置已应用', 'success');
            }
            
            // 更新状态显示
            updateAPIStatus();
            
            // 隐藏配置面板
            setTimeout(hideConfigPanel, 1500);
        }

        // 加载保存的API配置
        function loadAPIConfig() {
            try {
                const savedConfig = localStorage.getItem('aiSuShiAPIConfig');
                if (savedConfig) {
                    API_CONFIG = JSON.parse(savedConfig);
                    API_CONFIG.isConfigured = true;
                    updateAPIStatus();
                    showStatus('已加载保存的API配置', 'success');
                }
            } catch (error) {
                console.error('加载API配置失败:', error);
                showStatus('加载配置失败', 'error');
            }
        }

        // 获取默认模型名称
        function getDefaultModel(provider) {
            switch(provider) {
                case 'openai': return 'gpt-3.5-turbo';
                case 'tencent': return 'hunyuan-pro';
                case 'baidu': return 'ERNIE-Bot';
                case 'iflytek': return 'spark-3.5';
                case 'zhipu': return 'chatglm_pro';
                default: return '';
            }
        }

        // 更新API状态显示
        function updateAPIStatus() {
            if (API_CONFIG.isConfigured) {
                let providerName = '';
                switch(API_CONFIG.provider) {
                    case 'tencent': providerName = '腾讯混元'; break;
                    case 'baidu': providerName = '百度文心一言'; break;
                    case 'iflytek': providerName = '讯飞星火'; break;
                    case 'zhipu': providerName = '智谱ChatGLM'; break;
                    default: providerName = API_CONFIG.provider;
                }
                
                apiStatus.textContent = `${providerName} API已配置`;
                apiStatus.className = 'text-green-600';
            } else {
                apiStatus.textContent = '未配置API';
                apiStatus.className = 'text-gray-500';
            }
        }

        // 显示状态指示器
        function showStatus(message, type = 'info') {
            statusIndicator.textContent = message;
            
            // 设置颜色
            switch(type) {
                case 'success':
                    statusIndicator.className = 'fixed bottom-4 right-4 px-3 py-1 rounded-full text-xs text-white bg-green-600 opacity-100 transition-opacity duration-300';
                    break;
                case 'error':
                    statusIndicator.className = 'fixed bottom-4 right-4 px-3 py-1 rounded-full text-xs text-white bg-red-600 opacity-100 transition-opacity duration-300';
                    break;
                case 'loading':
                    statusIndicator.className = 'fixed bottom-4 right-4 px-3 py-1 rounded-full text-xs text-white bg-blue-600 opacity-100 transition-opacity duration-300';
                    break;
                default:
                    statusIndicator.className = 'fixed bottom-4 right-4 px-3 py-1 rounded-full text-xs text-white bg-gray-600 opacity-100 transition-opacity duration-300';
            }
            
            // 3秒后自动隐藏
            setTimeout(() => {
                statusIndicator.classList.replace('opacity-100', 'opacity-0');
            }, 3000);
        }

        // 处理发送消息 - 恢复真实AI调用
        async function handleSendMessage() {
            console.log('handleSendMessage函数被调用');
            
            try {
                const message = userInput.value.trim();
                console.log('用户输入:', message);
                
                if (!message) {
                    console.log('消息为空，不发送');
                    return;
                }
                
                // 添加用户消息
                addUserMessage(message);
                userInput.value = '';
                
                // 显示"正在输入"状态
                showTypingIndicator();
                
                // 调用真实AI API
                try {
                    showStatus('正在调用腾讯云混元大模型...', 'loading');
                    
                    // 直接调用腾讯云API
                    const reply = await callTencentAPI([
                        { role: 'system', content: AI_SU_SHI_PROMPT },
                        { role: 'user', content: message }
                    ]);
                    
                    console.log('API返回的原始回复:', reply);
                    console.log('回复类型:', typeof reply);
                    
                    // 隐藏"正在输入"状态并显示回复
                    hideTypingIndicator();
                    addAIReply(reply);
                    
                    showStatus('AI回复已生成', 'success');
                } catch (apiError) {
                    console.error('获取AI回复失败:', apiError);
                    hideTypingIndicator();
                    
                    // 显示错误信息和默认回复
                    showStatus('API调用失败，使用默认回复', 'error');
                    const errorMessage = 'API调用失败，此为默认回复。错误详情：' + apiError.message;
                    console.log(errorMessage);
                    addAIReply(getRandomDefaultReply() + '\n\n（注：' + errorMessage + '）');
                }
                
            } catch (error) {
                console.error('发送消息时出错:', error);
                hideTypingIndicator();
                showStatus('发送失败', 'error');
            }
        }

        // 调用AI API
        async function callAIAPI(userMessage) {
            // 构建对话历史
            const messages = [
                { role: 'system', content: AI_SU_SHI_PROMPT },
                { role: 'user', content: userMessage }
            ];
            
            // 根据不同的API提供商构建请求
            switch(API_CONFIG.provider) {
                case 'openai':
                    return await callOpenAICompatibleAPI(messages);
                case 'tencent':
                    return await callTencentAPI(messages);
                case 'baidu':
                    return await callBaiduAPI(messages);
                case 'iflytek':
                    return await callIflytekAPI(messages);
                case 'zhipu':
                    return await callZhipuAPI(messages);
                default:
                    throw new Error('不支持的API提供商');
            }
        }

        // 调用腾讯云混元大模型API
        async function callTencentAPI(messages) {
            // 构建符合腾讯云tokenhub API格式的请求数据
            const requestData = {
                model: API_CONFIG.model,
                system: AI_SU_SHI_PROMPT,
                messages: messages.slice(1), // 移除system消息，因为已经在system字段中
                stream: false,
                temperature: 0.7,
                top_p: 0.9
            };
            
            console.log('调用腾讯云混元大模型API:', {
                endpoint: API_CONFIG.endpoint,
                model: API_CONFIG.model,
                messages: requestData.messages.length,
                requestData: requestData
            });
            
            try {
                const response = await fetch(API_CONFIG.endpoint, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                        'Authorization': `Bearer ${API_CONFIG.apiKey}`
                    },
                    body: JSON.stringify(requestData)
                });
                
                // 记录响应状态
                console.log('API响应状态:', response.status);
                
                // 读取响应内容
                const responseText = await response.text();
                console.log('API响应内容:', responseText);
                
                if (!response.ok) {
                    throw new Error(`腾讯云API请求失败: ${response.status} ${responseText}`);
                }
                
                try {
                    const data = JSON.parse(responseText);
                    console.log('解析后的响应数据:', data);
                    
                    // 检查响应格式
                    if (data.content) {
                        console.log('从data.content获取回复:', data.content);
                        return data.content;
                    } else if (data.choices && data.choices[0] && data.choices[0].message) {
                        console.log('从data.choices获取回复:', data.choices[0].message.content);
                        return data.choices[0].message.content;
                    } else if (data.message) {
                        console.log('从data.message获取回复:', data.message);
                        return data.message;
                    } else if (Array.isArray(data) && data.length > 0 && data[0].type === 'text') {
                        // 处理数组格式的响应：[{type: "text", text: "内容"}]
                        console.log('从数组格式响应获取回复:', data[0].text);
                        return data[0].text;
                    } else {
                        console.log('响应格式不符合预期，返回完整响应对象');
                        return data;
                    }
                } catch (parseError) {
                    console.error('解析JSON响应失败:', parseError);
                    console.log('原始响应文本:', responseText);
                    throw new Error(`解析API响应失败: ${parseError.message}`);
                }
            } catch (error) {
                console.error('腾讯云API调用详细错误:', error);
                
                // 提供更详细的错误信息
                if (error.message.includes('401')) {
                    throw new Error('API密钥无效或已过期，请检查您的API密钥');
                } else if (error.message.includes('429')) {
                    throw new Error('API调用频率过高，请稍后再试');
                } else if (error.message.includes('404')) {
                    throw new Error('API端点不存在，请检查端点配置');
                } else if (error.message.includes('NetworkError') || error.message.includes('fetch')) {
                    throw new Error('网络连接错误，请检查您的网络连接');
                } else {
                    throw error;
                }
            }
        }

        // 调用百度文心一言API
        async function callBaiduAPI(messages) {
            // 百度API需要access_token
            // 这里简化处理，实际使用时需要先获取access_token
            const accessToken = API_CONFIG.secretKey || API_CONFIG.apiKey;
            
            const requestData = {
                model: API_CONFIG.model,
                messages: messages,
                temperature: 0.7,
                top_p: 0.9,
                max_tokens: 1000
            };
            
            const response = await fetch(`${API_CONFIG.endpoint}?access_token=${accessToken}`, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(requestData)
            });
            
            if (!response.ok) {
                throw new Error(`百度API请求失败: ${response.status} ${await response.text()}`);
            }
            
            const data = await response.json();
            return data.result;
        }

        // 调用讯飞星火API
        async function callIflytekAPI(messages) {
            // 讯飞API需要特殊的请求格式
            const requestData = {
                model: API_CONFIG.model,
                messages: messages,
                temperature: 0.7,
                top_p: 0.9,
                max_tokens: 1000
            };
            
            const response = await fetch(API_CONFIG.endpoint, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    'Authorization': `Bearer ${API_CONFIG.apiKey}`
                },
                body: JSON.stringify(requestData)
            });
            
            if (!response.ok) {
                throw new Error(`讯飞API请求失败: ${response.status} ${await response.text()}`);
            }
            
            const data = await response.json();
            return data.choices[0].message.content;
        }

        // 调用智谱ChatGLM API
        async function callZhipuAPI(messages) {
            const requestData = {
                model: API_CONFIG.model,
                messages: messages,
                temperature: 0.7,
                top_p: 0.9,
                max_tokens: 1000
            };
            
            const response = await fetch(API_CONFIG.endpoint, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    'Authorization': `Bearer ${API_CONFIG.apiKey}`
                },
                body: JSON.stringify(requestData)
            });
            
            if (!response.ok) {
                throw new Error(`智谱API请求失败: ${response.status} ${await response.text()}`);
            }
            
            const data = await response.json();
            return data.choices[0].message.content;
        }
        
        // 调用OpenAI兼容API（支持各种兼容OpenAI API格式的服务）
        async function callOpenAICompatibleAPI(messages) {
            // 使用用户提供的API密钥
            const apiKey = API_CONFIG.apiKey;
            
            // 如果用户没有指定端点，使用默认的OpenAI端点
            const endpoint = API_CONFIG.endpoint || 'https://api.openai.com/v1/chat/completions';
            
            // 如果用户没有指定模型，使用默认模型
            const model = API_CONFIG.model || 'gpt-3.5-turbo';
            
            const requestData = {
                model: model,
                messages: messages,
                temperature: 0.7,
                top_p: 0.9,
                max_tokens: 1000
            };
            
            console.log('调用OpenAI兼容API:', {
                endpoint: endpoint,
                model: model,
                messages: messages.length
            });
            
            try {
                const response = await fetch(endpoint, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                        'Authorization': `Bearer ${apiKey}`
                    },
                    body: JSON.stringify(requestData)
                });
                
                // 记录响应状态
                console.log('API响应状态:', response.status);
                
                // 读取响应内容
                const responseText = await response.text();
                console.log('API响应内容:', responseText);
                
                if (!response.ok) {
                    throw new Error(`OpenAI兼容API请求失败: ${response.status} ${responseText}`);
                }
                
                const data = JSON.parse(responseText);
                
                if (!data.choices || !data.choices[0] || !data.choices[0].message) {
                    throw new Error('API响应格式不正确');
                }
                
                return data.choices[0].message.content;
            } catch (error) {
                console.error('OpenAI兼容API调用详细错误:', error);
                
                // 提供更详细的错误信息
                if (error.message.includes('401')) {
                    throw new Error('API密钥无效或已过期，请检查您的API密钥');
                } else if (error.message.includes('429')) {
                    throw new Error('API调用频率过高，请稍后再试');
                } else if (error.message.includes('404')) {
                    throw new Error('API端点不存在，请检查端点配置');
                } else if (error.message.includes('NetworkError') || error.message.includes('fetch')) {
                    throw new Error('网络连接错误，请检查您的网络连接');
                } else {
                    throw error;
                }
            }
        }

        // 添加用户消息到聊天历史
        function addUserMessage(message) {
            const userMessageHTML = `
                <div class="flex justify-end mb-8 fade-in">
                    <div class="chat-bubble-user bg-gray-100 p-6 max-w-[80%]">
                        <p class="font-song text-gray-800 leading-relaxed text-lg">${escapeHtml(message)}</p>
                    </div>
                    <div class="flex-shrink-0 ml-4">
                        <div class="w-14 h-14 rounded-full bg-gray-400 flex items-center justify-center text-white shadow-lg hover:scale-105 transition-transform duration-300">
                            <i class="fa fa-user text-2xl"></i>
                        </div>
                    </div>
                </div>
            `;
            chatHistory.insertAdjacentHTML('beforeend', userMessageHTML);
            chatHistory.scrollTop = chatHistory.scrollHeight;
        }

        // 添加AI苏轼消息到聊天历史
        function addAIReply(message) {
            // 确保message是字符串，如果是对象则转换为JSON字符串
            let replyText = message;
            if (typeof message === 'object') {
                try {
                    // 检查是否为数组格式：[{type: "text", text: "内容"}]
                    if (Array.isArray(message) && message.length > 0 && message[0].type === 'text') {
                        replyText = message[0].text;
                        console.log('检测到数组格式响应，提取text内容:', replyText);
                    } else {
                        replyText = JSON.stringify(message, null, 2);
                        console.log('将对象转换为字符串:', replyText);
                    }
                } catch (e) {
                    replyText = String(message);
                    console.log('对象转换失败，使用String():', replyText);
                }
            }
            
            const aiMessageHTML = `
                <div class="flex mb-6 fade-in">
                    <div class="flex-shrink-0 mr-4">
                        <div class="w-14 h-14 rounded-full bg-primary flex items-center justify-center text-white shadow-lg border-2 border-secondary/50 hover:scale-105 transition-transform duration-300">
                            <span class="text-2xl font-bold font-kai">苏</span>
                        </div>
                    </div>
                    <div class="chat-bubble-ai bg-secondary p-6 max-w-[80%]">
                        <p class="text-dark whitespace-pre-wrap">${escapeHtml(replyText)}</p>
                    </div>
                </div>
            `;
            chatHistory.insertAdjacentHTML('beforeend', aiMessageHTML);
            chatHistory.scrollTop = chatHistory.scrollHeight;
        }

        // 显示"正在输入"状态
        function showTypingIndicator() {
            const typingHTML = `
                <div id="typing-indicator" class="flex mb-6 fade-in">
                    <div class="flex-shrink-0 mr-4">
                        <div class="w-14 h-14 rounded-full bg-primary flex items-center justify-center text-white shadow-lg border-2 border-secondary/50 hover:scale-105 transition-transform duration-300">
                            <span class="text-2xl font-bold font-kai">苏</span>
                        </div>
                    </div>
                    <div class="chat-bubble-ai bg-secondary p-6 max-w-[80%]">
                        <div class="flex space-x-2">
                            <div class="w-2 h-2 rounded-full bg-gray-600 animate-bounce"></div>
                            <div class="w-2 h-2 rounded-full bg-gray-600 animate-bounce" style="animation-delay: 0.2s"></div>
                            <div class="w-2 h-2 rounded-full bg-gray-600 animate-bounce" style="animation-delay: 0.4s"></div>
                        </div>
                    </div>
                </div>
            `;
            chatHistory.insertAdjacentHTML('beforeend', typingHTML);
            chatHistory.scrollTop = chatHistory.scrollHeight;
        }

        // 隐藏"正在输入"状态
        function hideTypingIndicator() {
            const typingIndicator = document.getElementById('typing-indicator');
            if (typingIndicator) {
                typingIndicator.remove();
            }
        }

        // 获取随机默认回复
        function getRandomDefaultReply() {
            const index = Math.floor(Math.random() * defaultReplies.length);
            return defaultReplies[index];
        }

        // HTML转义
        function escapeHtml(text) {
            const div = document.createElement('div');
            div.textContent = text;
            return div.innerHTML;
        }

        // 页面加载完成后初始化
        document.addEventListener('DOMContentLoaded', init);
    </script>
</body>
</html>
