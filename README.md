[1.html](https://github.com/user-attachments/files/26569219/1.html)
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI工具学习与景观业务结合汇报</title>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+SC:wght@300;400;500;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --deep-blue: #0a1628;
            --tech-blue: #1e3a5f;
            --light-blue: #4a90d9;
            --accent-blue: #00d4ff;
            --accent-purple: #a855f7;
            --accent-green: #10b981;
            --accent-orange: #f59e0b;
            --accent-pink: #ec4899;
            --silver-gray: #c0c8d4;
            --dark-gray: #1a2436;
        }

        body {
            font-family: 'Noto Sans SC', sans-serif;
            background: var(--deep-blue);
            color: #e8edf5;
            line-height: 1.8;
            overflow-x: hidden;
        }

        /* 背景动效 */
        .bg-particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
            overflow: hidden;
        }

        .particle {
            position: absolute;
            border-radius: 50%;
            animation: float 15s infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(100vh) rotate(0deg); opacity: 0; }
            10% { opacity: 0.6; }
            90% { opacity: 0.6; }
            100% { transform: translateY(-100vh) rotate(720deg); opacity: 0; }
        }

        /* 网格线背景 */
        .grid-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: 
                linear-gradient(rgba(0, 212, 255, 0.03) 1px, transparent 1px),
                linear-gradient(90deg, rgba(0, 212, 255, 0.03) 1px, transparent 1px);
            background-size: 50px 50px;
            z-index: 0;
        }

        /* 背景圆环装饰 */
        .bg-rings {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            pointer-events: none;
            z-index: 0;
        }

        .ring {
            position: absolute;
            border: 1px solid rgba(0, 212, 255, 0.1);
            border-radius: 50%;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            animation: ring-pulse 8s ease-in-out infinite;
        }

        .ring:nth-child(1) { width: 300px; height: 300px; animation-delay: 0s; }
        .ring:nth-child(2) { width: 500px; height: 500px; animation-delay: 1s; }
        .ring:nth-child(3) { width: 700px; height: 700px; animation-delay: 2s; }
        .ring:nth-child(4) { width: 900px; height: 900px; animation-delay: 3s; }

        @keyframes ring-pulse {
            0%, 100% { opacity: 0.1; transform: translate(-50%, -50%) scale(1); }
            50% { opacity: 0.3; transform: translate(-50%, -50%) scale(1.05); }
        }

        /* 内容区域 */
        .container {
            position: relative;
            z-index: 1;
            max-width: 1100px;
            margin: 0 auto;
            padding: 40px 30px 80px;
        }

        /* 头部区域 */
        .header {
            text-align: center;
            padding: 60px 20px 50px;
            margin-bottom: 50px;
            position: relative;
        }

        .header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 400px;
            height: 400px;
            background: radial-gradient(circle, rgba(0, 212, 255, 0.15) 0%, transparent 70%);
            border-radius: 50%;
            animation: pulse 4s ease-in-out infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: translateX(-50%) scale(1); opacity: 0.5; }
            50% { transform: translateX(-50%) scale(1.3); opacity: 0.8; }
        }

        .header-icon {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            width: 100px;
            height: 100px;
            background: linear-gradient(135deg, var(--tech-blue), var(--accent-blue));
            border-radius: 25px;
            margin-bottom: 25px;
            box-shadow: 0 10px 40px rgba(0, 212, 255, 0.3);
            animation: float-icon 3s ease-in-out infinite;
            position: relative;
        }

        @keyframes float-icon {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }

        .header-icon i {
            font-size: 45px;
            color: #fff;
        }

        .header h1 {
            font-size: 2.5rem;
            font-weight: 700;
            background: linear-gradient(135deg, #fff 0%, var(--accent-blue) 50%, var(--light-blue) 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 20px;
            letter-spacing: 2px;
            position: relative;
        }

        .header-line {
            width: 150px;
            height: 4px;
            background: linear-gradient(90deg, transparent, var(--accent-blue), transparent);
            margin: 0 auto 25px;
            border-radius: 2px;
        }

        .header-meta {
            display: flex;
            justify-content: center;
            gap: 40px;
            margin-top: 20px;
            flex-wrap: wrap;
        }

        .meta-item {
            display: flex;
            align-items: center;
            gap: 10px;
            color: var(--silver-gray);
            font-size: 0.95rem;
        }

        .meta-item i {
            color: var(--accent-blue);
            font-size: 1.1rem;
        }

        /* 统计卡片 */
        .stats-row {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 50px;
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .stats-row.visible {
            opacity: 1;
            transform: translateY(0);
        }

        .stat-card {
            background: linear-gradient(145deg, rgba(30, 58, 95, 0.5) 0%, rgba(26, 36, 54, 0.7) 100%);
            border: 1px solid rgba(0, 212, 255, 0.15);
            border-radius: 16px;
            padding: 25px;
            text-align: center;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .stat-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 3px;
            background: var(--card-accent, var(--accent-blue));
        }

        .stat-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 40px rgba(0, 212, 255, 0.15);
            border-color: rgba(0, 212, 255, 0.4);
        }

        .stat-icon {
            width: 50px;
            height: 50px;
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 15px;
            background: rgba(0, 212, 255, 0.1);
        }

        .stat-icon i {
            font-size: 24px;
            color: var(--card-accent, var(--accent-blue));
        }

        .stat-number {
            font-size: 2rem;
            font-weight: 700;
            color: #fff;
            margin-bottom: 5px;
        }

        .stat-label {
            font-size: 0.9rem;
            color: var(--silver-gray);
        }

        /* 引言区域 */
        .intro {
            background: linear-gradient(145deg, rgba(30, 58, 95, 0.5) 0%, rgba(26, 36, 54, 0.7) 100%);
            border-left: 4px solid var(--accent-blue);
            border-radius: 0 20px 20px 0;
            padding: 35px 40px;
            margin-bottom: 50px;
            position: relative;
            opacity: 0;
            transform: translateX(-30px);
            transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .intro.visible {
            opacity: 1;
            transform: translateX(0);
        }

        .intro::before {
            content: '"';
            position: absolute;
            top: 10px;
            left: 15px;
            font-size: 80px;
            color: rgba(0, 212, 255, 0.1);
            font-family: Georgia, serif;
            line-height: 1;
        }

        .intro-text {
            font-size: 1.1rem;
            line-height: 2;
            color: #d0dae8;
        }

        .intro-highlight {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            background: linear-gradient(90deg, rgba(0, 212, 255, 0.15), transparent);
            padding: 5px 15px;
            border-radius: 20px;
            margin-top: 20px;
            color: var(--accent-blue);
            font-weight: 500;
        }

        .intro-highlight i {
            font-size: 1.1rem;
        }

        /* 章节卡片 */
        .section-card {
            background: linear-gradient(145deg, rgba(30, 58, 95, 0.4) 0%, rgba(26, 36, 54, 0.6) 100%);
            border: 1px solid rgba(0, 212, 255, 0.15);
            border-radius: 24px;
            padding: 45px;
            margin-bottom: 45px;
            backdrop-filter: blur(10px);
            position: relative;
            overflow: hidden;
            opacity: 0;
            transform: translateY(40px);
            transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .section-card.visible {
            opacity: 1;
            transform: translateY(0);
        }

        .section-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 3px;
            background: linear-gradient(90deg, var(--accent-blue), var(--light-blue), var(--accent-purple), var(--accent-blue));
            background-size: 300% 100%;
            animation: shimmer 4s linear infinite;
        }

        @keyframes shimmer {
            0% { background-position: -300% 0; }
            100% { background-position: 300% 0; }
        }

        /* 章节标签 */
        .section-badge {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            background: rgba(0, 212, 255, 0.1);
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 0.85rem;
            color: var(--accent-blue);
            margin-bottom: 20px;
        }

        .section-badge i {
            font-size: 0.9rem;
        }

        /* 章节标题 */
        .section-title {
            font-size: 1.7rem;
            font-weight: 600;
            color: #fff;
            margin-bottom: 30px;
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .section-number {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            width: 55px;
            height: 55px;
            background: linear-gradient(135deg, var(--accent-blue) 0%, var(--tech-blue) 100%);
            border-radius: 15px;
            font-size: 1.4rem;
            font-weight: 700;
            box-shadow: 0 4px 25px rgba(0, 212, 255, 0.3);
            flex-shrink: 0;
        }

        .section-content {
            position: relative;
            z-index: 1;
        }

        /* 描述文字 */
        .section-desc {
            color: var(--silver-gray);
            font-size: 1rem;
            margin-bottom: 30px;
            padding-left: 15px;
            border-left: 2px solid rgba(0, 212, 255, 0.3);
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .section-desc i {
            color: var(--accent-blue);
        }

        /* 子卡片 */
        .subsection-card {
            background: rgba(26, 36, 54, 0.5);
            border: 1px solid rgba(0, 212, 255, 0.08);
            border-radius: 16px;
            padding: 28px;
            margin-bottom: 25px;
            transition: all 0.3s ease;
            position: relative;
        }

        .subsection-card:hover {
            border-color: rgba(0, 212, 255, 0.25);
            transform: translateX(5px);
            background: rgba(30, 58, 95, 0.3);
        }

        .subsection-card:last-child {
            margin-bottom: 0;
        }

        .subsection-header {
            display: flex;
            align-items: center;
            gap: 15px;
            margin-bottom: 18px;
        }

        .subsection-icon {
            width: 45px;
            height: 45px;
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-shrink: 0;
        }

        .subsection-icon.blue { background: rgba(59, 130, 246, 0.15); color: #3b82f6; }
        .subsection-icon.green { background: rgba(16, 185, 129, 0.15); color: #10b981; }
        .subsection-icon.purple { background: rgba(168, 85, 247, 0.15); color: #a855f7; }
        .subsection-icon.orange { background: rgba(245, 158, 11, 0.15); color: #f59e0b; }
        .subsection-icon.pink { background: rgba(236, 72, 153, 0.15); color: #ec4899; }

        .subsection-icon i {
            font-size: 20px;
        }

        .subsection-title {
            font-size: 1.2rem;
            font-weight: 600;
            color: #fff;
        }

        .subsection-content {
            color: #b8c5d6;
            font-size: 1rem;
            line-height: 1.9;
            padding-left: 60px;
        }

        /* 重点内容高亮 */
        .highlight {
            background: linear-gradient(90deg, rgba(0, 212, 255, 0.15), transparent);
            padding: 2px 8px;
            border-radius: 4px;
            color: var(--accent-blue);
            font-weight: 500;
        }

        .highlight-purple {
            background: linear-gradient(90deg, rgba(168, 85, 247, 0.15), transparent);
            color: #c084fc;
        }

        .highlight-green {
            background: linear-gradient(90deg, rgba(16, 185, 129, 0.15), transparent);
            color: #34d399;
        }

        .highlight-orange {
            background: linear-gradient(90deg, rgba(245, 158, 11, 0.15), transparent);
            color: #fbbf24;
        }

        /* 标签列表 */
        .tag-list {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 15px;
        }

        .tag {
            display: inline-flex;
            align-items: center;
            gap: 6px;
            background: rgba(0, 212, 255, 0.08);
            border: 1px solid rgba(0, 212, 255, 0.15);
            padding: 6px 14px;
            border-radius: 20px;
            font-size: 0.85rem;
            color: var(--silver-gray);
            transition: all 0.3s ease;
        }

        .tag:hover {
            background: rgba(0, 212, 255, 0.15);
            color: var(--accent-blue);
            transform: translateY(-2px);
        }

        .tag i {
            font-size: 0.8rem;
            color: var(--accent-blue);
        }

        /* 进度条 */
        .progress-list {
            margin-top: 20px;
        }

        .progress-item {
            margin-bottom: 20px;
        }

        .progress-item:last-child {
            margin-bottom: 0;
        }

        .progress-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 8px;
        }

        .progress-label {
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 0.95rem;
            color: #b8c5d6;
        }

        .progress-label i {
            color: var(--accent-blue);
            font-size: 0.9rem;
        }

        .progress-value {
            font-size: 0.9rem;
            color: var(--accent-blue);
            font-weight: 500;
        }

        .progress-bar {
            height: 8px;
            background: rgba(0, 212, 255, 0.1);
            border-radius: 4px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--accent-blue), var(--light-blue));
            border-radius: 4px;
            transition: width 1s ease-out;
        }

        /* 两栏布局 */
        .two-column {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
            margin-top: 25px;
        }

        .column-card {
            background: rgba(30, 58, 95, 0.35);
            border: 1px solid rgba(0, 212, 255, 0.12);
            border-radius: 18px;
            padding: 28px;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .column-card::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 4px;
            height: 100%;
            background: var(--column-accent, var(--accent-blue));
        }

        .column-card:hover {
            border-color: rgba(0, 212, 255, 0.35);
            transform: translateY(-5px);
            box-shadow: 0 15px 40px rgba(0, 212, 255, 0.1);
        }

        .column-header {
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 18px;
        }

        .column-icon {
            width: 40px;
            height: 40px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            background: rgba(0, 212, 255, 0.12);
        }

        .column-icon i {
            font-size: 18px;
            color: var(--column-accent, var(--accent-blue));
        }

        .column-title {
            font-size: 1.15rem;
            font-weight: 600;
            color: #fff;
        }

        .column-body {
            color: #a0aec0;
            font-size: 0.95rem;
            line-height: 1.9;
        }

        .column-body ul {
            list-style: none;
            padding: 0;
        }

        .column-body li {
            padding: 10px 0;
            padding-left: 28px;
            position: relative;
            border-bottom: 1px solid rgba(0, 212, 255, 0.05);
        }

        .column-body li:last-child {
            border-bottom: none;
        }

        .column-body li::before {
            content: '▸';
            position: absolute;
            left: 5px;
            color: var(--column-accent, var(--accent-blue));
            font-size: 0.85rem;
        }

        .column-body strong {
            color: #d0dae8;
        }

        /* 虚拟角色卡片 */
        .role-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 20px;
            margin-top: 25px;
        }

        .role-card {
            background: linear-gradient(145deg, rgba(30, 58, 95, 0.5) 0%, rgba(26, 36, 54, 0.6) 100%);
            border: 1px solid rgba(0, 212, 255, 0.1);
            border-radius: 16px;
            padding: 25px;
            text-align: center;
            transition: all 0.3s ease;
        }

        .role-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 20px 50px rgba(0, 212, 255, 0.15);
            border-color: rgba(0, 212, 255, 0.4);
        }

        .role-avatar {
            width: 70px;
            height: 70px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 18px;
            font-size: 28px;
        }

        .role-avatar.blue { background: linear-gradient(135deg, #3b82f6, #1d4ed8); }
        .role-avatar.purple { background: linear-gradient(135deg, #a855f7, #7c3aed); }
        .role-avatar.green { background: linear-gradient(135deg, #10b981, #059669); }

        .role-name {
            font-size: 1.1rem;
            font-weight: 600;
            color: #fff;
            margin-bottom: 8px;
        }

        .role-desc {
            font-size: 0.85rem;
            color: var(--silver-gray);
            line-height: 1.6;
        }

        /* 协作流程 */
        .flow-diagram {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
            margin-top: 30px;
            flex-wrap: wrap;
            padding: 25px;
            background: rgba(26, 36, 54, 0.4);
            border-radius: 16px;
        }

        .flow-step {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 10px;
        }

        .flow-icon {
            width: 55px;
            height: 55px;
            border-radius: 14px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 22px;
        }

        .flow-icon.blue { background: rgba(59, 130, 246, 0.15); color: #3b82f6; }
        .flow-icon.purple { background: rgba(168, 85, 247, 0.15); color: #a855f7; }
        .flow-icon.green { background: rgba(16, 185, 129, 0.15); color: #10b981; }
        .flow-icon.orange { background: rgba(245, 158, 11, 0.15); color: #f59e0b; }

        .flow-label {
            font-size: 0.85rem;
            color: var(--silver-gray);
            text-align: center;
        }

        .flow-arrow {
            color: var(--accent-blue);
            font-size: 24px;
            opacity: 0.6;
        }

        /* 结尾区域 */
        .conclusion {
            text-align: center;
            padding: 50px 40px;
            background: linear-gradient(145deg, rgba(30, 58, 95, 0.4) 0%, rgba(26, 36, 54, 0.6) 100%);
            border-radius: 24px;
            border: 1px solid rgba(0, 212, 255, 0.15);
            margin-top: 50px;
            position: relative;
            overflow: hidden;
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .conclusion.visible {
            opacity: 1;
            transform: translateY(0);
        }

        .conclusion::before {
            content: '';
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 200px;
            height: 200px;
            background: radial-gradient(circle, rgba(0, 212, 255, 0.1) 0%, transparent 70%);
        }

        .conclusion-icon {
            width: 70px;
            height: 70px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--accent-blue), var(--tech-blue));
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 25px;
            font-size: 28px;
            box-shadow: 0 10px 30px rgba(0, 212, 255, 0.3);
        }

        .conclusion-text {
            font-size: 1.1rem;
            color: #b8c5d6;
            max-width: 800px;
            margin: 0 auto;
            position: relative;
            line-height: 1.9;
        }

        /* 底部装饰 */
        .footer-decoration {
            text-align: center;
            margin-top: 60px;
            padding: 40px 0;
            position: relative;
        }

        .footer-decoration::before {
            content: '';
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 60%;
            height: 1px;
            background: linear-gradient(90deg, transparent, rgba(0, 212, 255, 0.3), transparent);
        }

        .footer-icons {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-bottom: 20px;
        }

        .footer-icon {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            background: rgba(0, 212, 255, 0.08);
            border: 1px solid rgba(0, 212, 255, 0.15);
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--accent-blue);
            font-size: 18px;
            transition: all 0.3s ease;
        }

        .footer-icon:hover {
            background: rgba(0, 212, 255, 0.2);
            transform: translateY(-3px);
        }

        .footer-text {
            color: rgba(192, 200, 212, 0.5);
            font-size: 0.85rem;
        }

        /* 滚动条样式 */
        ::-webkit-scrollbar {
            width: 8px;
        }

        ::-webkit-scrollbar-track {
            background: var(--deep-blue);
        }

        ::-webkit-scrollbar-thumb {
            background: var(--tech-blue);
            border-radius: 4px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: var(--light-blue);
        }

        /* 响应式 */
        @media (max-width: 768px) {
            .header h1 {
                font-size: 1.6rem;
            }

            .section-card {
                padding: 30px 22px;
            }

            .section-title {
                font-size: 1.3rem;
                flex-direction: column;
                align-items: flex-start;
                gap: 12px;
            }

            .two-column {
                grid-template-columns: 1fr;
            }

            .subsection-content {
                padding-left: 0;
                margin-top: 15px;
            }

            .stats-row {
                grid-template-columns: repeat(2, 1fr);
            }

            .flow-diagram {
                flex-direction: column;
            }

            .flow-arrow {
                transform: rotate(90deg);
            }

            .role-cards {
                grid-template-columns: 1fr;
            }
        }

        /* 加载动画 */
        .loading-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--deep-blue);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 9999;
            transition: opacity 0.5s ease, visibility 0.5s ease;
        }

        .loading-overlay.hidden {
            opacity: 0;
            visibility: hidden;
        }

        .loader {
            width: 60px;
            height: 60px;
            border: 3px solid rgba(0, 212, 255, 0.1);
            border-top-color: var(--accent-blue);
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        /* 时间戳 */
        .timestamp {
            position: absolute;
            top: 20px;
            right: 25px;
            color: rgba(0, 212, 255, 0.4);
            font-size: 0.8rem;
            font-weight: 300;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .timestamp i {
            font-size: 0.75rem;
        }
    </style>
</head>
<body>
    <!-- 加载动画 -->
    <div class="loading-overlay" id="loadingOverlay">
        <div class="loader"></div>
    </div>

    <!-- 背景效果 -->
    <div class="grid-bg"></div>
    <div class="bg-particles" id="particles"></div>
    <div class="bg-rings">
        <div class="ring"></div>
        <div class="ring"></div>
        <div class="ring"></div>
        <div class="ring"></div>
    </div>

    <div class="container">
        <!-- 标题区域 -->
        <header class="header">
            <div class="header-icon">
                <i class="fas fa-robot"></i>
            </div>
            <h1>关于近两周 AI 工具学习与景观业务结合的初步汇报</h1>
            <div class="header-line"></div>
            <div class="header-meta">
                <div class="meta-item">
                    <i class="fas fa-calendar-alt"></i>
                    <span>2026年4月</span>
                </div>
                <div class="meta-item">
                    <i class="fas fa-user-astronaut"></i>
                    <span>个人学习汇报</span>
                </div>
                <div class="meta-item">
                    <i class="fas fa-leaf"></i>
                    <span>景观设计业务</span>
                </div>
            </div>
        </header>

        <!-- 统计数据 -->
        <div class="stats-row" id="statsRow">
            <div class="stat-card" style="--card-accent: #3b82f6;">
                <div class="stat-icon"><i class="fas fa-tools"></i></div>
                <div class="stat-number">5+</div>
                <div class="stat-label">工具实测</div>
            </div>
            <div class="stat-card" style="--card-accent: #a855f7;">
                <div class="stat-icon"><i class="fas fa-brain"></i></div>
                <div class="stat-number">3</div>
                <div class="stat-label">AI模型测试</div>
            </div>
            <div class="stat-card" style="--card-accent: #10b981;">
                <div class="stat-icon"><i class="fas fa-rocket"></i></div>
                <div class="stat-number">4</div>
                <div class="stat-label">技能掌握</div>
            </div>
            <div class="stat-card" style="--card-accent: #f59e0b;">
                <div class="stat-icon"><i class="fas fa-chart-line"></i></div>
                <div class="stat-number">2</div>
                <div class="stat-label">阶段规划</div>
            </div>
        </div>

        <!-- 引言 -->
        <div class="intro" id="intro">
            <p class="intro-text">
                最近两周的业余时间，我初步了解并实操了 OpenClaw、Workbuddy 等 AI Agent 工具。这次尝试给我最大的收获，其实是一种工作思维的转变。以前实习做项目，总觉得找意向图、整理案例等"体力活"就该自己熬夜干。但接触 Agent 后我发现，完全可以把 AI 当成我的"虚拟实习生"。我的主要精力应该放在"如何下达准确指令"以及"判断结果是否可用"上。这种从"纯画图"变成"小包工头"的效率思维，让我觉得非常有必要向您简单汇报一下近期的尝试与设想。
            </p>
            <div class="intro-highlight">
                <i class="fas fa-lightbulb"></i>
                核心理念：从"纯画图" → "小包工头"
            </div>
        </div>

        <!-- 第一部分 -->
        <div class="section-card" id="section1">
            <span class="timestamp"><i class="fas fa-microchip"></i> Part 01</span>
            <div class="section-badge"><i class="fas fa-cog"></i> 底层接口与配置</div>
            <h2 class="section-title">
                <span class="section-number">一</span>
                工具摸索与踩坑经验
            </h2>
            <div class="section-content">
                <p class="section-desc">
                    <i class="fas fa-info-circle"></i>
                    在初期的技术测试中，我经历了多次"折腾"，但也因此明确了适合我们的使用方式
                </p>

                <div class="subsection-card">
                    <div class="subsection-header">
                        <div class="subsection-icon blue"><i class="fas fa-server"></i></div>
                        <h3 class="subsection-title">算力分配（放弃本地，拥抱云端）</h3>
                    </div>
                    <div class="subsection-content">
                        <p>一开始我尝试在本地部署 Ollama（跑 Llama 3 等），但极其消耗电脑内存，导致画图时卡顿。因此现阶段建议弃用本地算力，直接调用云端 API 接口，保证工作流顺畅。</p>
                        <div class="tag-list">
                            <span class="tag"><i class="fas fa-ban"></i> 本地 Ollama</span>
                            <span class="tag"><i class="fas fa-check"></i> 云端 API</span>
                            <span class="tag"><i class="fas fa-bolt"></i> 流畅工作</span>
                        </div>
                    </div>
                </div>

                <div class="subsection-card">
                    <div class="subsection-header">
                        <div class="subsection-icon purple"><i class="fas fa-cubes"></i></div>
                        <h3 class="subsection-title">各家模型实测与组合使用</h3>
                    </div>
                    <div class="subsection-content">
                        <p>期间测试了多款模型，感觉国产 MiniMax，Qwen3.6模型性价比高；Claude 聪明但网络节点易封停；Gemini 在查资料和生图上体验很好。得出的结论是：需要根据<span class="highlight-purple">"查资料、写文本、配图"</span>等不同需求，组合接入不同大模型的接口，效果才最好。</p>
                    </div>
                </div>

                <div class="subsection-card">
                    <div class="subsection-header">
                        <div class="subsection-icon orange"><i class="fas fa-exclamation-triangle"></i></div>
                        <h3 class="subsection-title">认清"折腾成本"</h3>
                    </div>
                    <div class="subsection-content">
                        <p>这半个月遇到过刚配好的环境一更新就报错，也遇到过用爬虫抓图被网站封堵。OpenClaw学习速度赶不上升级速度，版本迭代迅速，目前刚体验4.6版本，出现系统崩溃UI界面卡顿，现象严重。这让我明白，搞技术工具的前期维护成本很高。如果未来要在团队推广，必须先剔除这些不稳定因素，拿出一个<span class="highlight-orange">"傻瓜式"</span>的稳定版本，避免增加大家的负担。</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- 第二部分 -->
        <div class="section-card" id="section2">
            <span class="timestamp"><i class="fas fa-microchip"></i> Part 02</span>
            <div class="section-badge"><i class="fas fa-puzzle-piece"></i> 框架与小技能</div>
            <h2 class="section-title">
                <span class="section-number">二</span>
                自动化流的初步跑通
            </h2>
            <div class="section-content">
                <p class="section-desc">
                    <i class="fas fa-info-circle"></i>
                    在明确了模型方向后，我跟着教程初步跑通了一些基础应用
                </p>

                <div class="subsection-card">
                    <div class="subsection-header">
                        <div class="subsection-icon blue"><i class="fas fa-id-card"></i></div>
                        <h3 class="subsection-title">了解运行机制与身份设定</h3>
                    </div>
                    <div class="subsection-content">
                        <p>初步弄懂了 Agent 的运转逻辑，能够通过修改 <span class="highlight">soul</span> 和 <span class="highlight">agents.md</span> 配置文件，给 AI 设定特定的"职业身份"来处理问题。</p>
                    </div>
                </div>

                <div class="subsection-card">
                    <div class="subsection-header">
                        <div class="subsection-icon green"><i class="fas fa-link"></i></div>
                        <h3 class="subsection-title">跨平台联动</h3>
                    </div>
                    <div class="subsection-content">
                        <p>试着安装了微信、飞书和 QQ 的插件，初步看懂了 AI 是如何联动这些聊天软件发送消息的。未来可以用飞书QQ等多Agent协调工作。</p>
                        <div class="tag-list">
                            <span class="tag"><i class="fab fa-weixin"></i> 微信插件</span>
                            <span class="tag"><i class="fas fa-paper-plane"></i> 飞书插件</span>
                            <span class="tag"><i class="fab fa-qq"></i> QQ 插件</span>
                        </div>
                    </div>
                </div>

                <div class="subsection-card">
                    <div class="subsection-header">
                        <div class="subsection-icon pink"><i class="fas fa-laptop-code"></i></div>
                        <h3 class="subsection-title">WorkBuddy 体验</h3>
                    </div>
                    <div class="subsection-content">
                        <p>在测试中发现 <span class="highlight-green">WorkBuddy 运行相对稳定</span>，非常契合日常办公场景。目前不仅熟悉了基础操作界面，还重点体验并筛选了多项 Skill 技能。例如，我配置了用于自我提升与学习总结的专属技能，它能帮助我快速提炼行业资讯和专业长文的核心观点，建立个人知识库；此外，我还尝试接入了小红书插件，用于快速抓取近期景观设计的爆款案例与大众反馈，为前期设计创意提供多维度的市场参考。目前仍在持续挖掘更多实用技能。</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- 第三部分 -->
        <div class="section-card" id="section3">
            <span class="timestamp"><i class="fas fa-microchip"></i> Part 03</span>
            <div class="section-badge"><i class="fas fa-bullseye"></i> 落地规划</div>
            <h2 class="section-title">
                <span class="section-number">三</span>
                结合景观设计业务的落地规划
            </h2>
            <div class="section-content">
                <p class="section-desc">
                    <i class="fas fa-info-circle"></i>
                    结合上述摸索，我认为这套工具可以在未来逐步赋能我们的景观设计工作，具体分为"个人辅助"与"团队共享"两个阶段的设想
                </p>

                <div class="two-column">
                    <div class="column-card" style="--column-accent: #3b82f6;">
                        <div class="column-header">
                            <div class="column-icon"><i class="fas fa-rocket"></i></div>
                            <span class="column-title">近期设想：个人工作流的提效</span>
                        </div>
                        <div class="column-body">
                            <ul>
                                <li><strong>配置"景观搜索小助手"</strong>：尝试写出一个能自动扒场地调研数据、查规范的专属 Skill，缩短前期找资料的时间。</li>
                                <li><strong>塞进日常工作流</strong>：前期让它辅助找灵感意向，中期帮着理顺文本的文字逻辑，后期尝试辅助优化排版。</li>
                            </ul>
                        </div>
                    </div>

                    <div class="column-card" style="--column-accent: #a855f7;">
                        <div class="column-header">
                            <div class="column-icon"><i class="fas fa-building"></i></div>
                            <span class="column-title">长远设想：搭建迷你的"AI 景观虚拟部门"</span>
                        </div>
                        <div class="column-body">
                            <p>如果基础操作固定下来，我希望能将其发展为团队共享的生产力工具。</p>
                        </div>
                    </div>
                </div>

                <!-- 虚拟员工角色 -->
                <div class="role-cards">
                    <div class="role-card">
                        <div class="role-avatar blue"><i class="fas fa-search"></i></div>
                        <div class="role-name">前期调研专员</div>
                        <div class="role-desc">自动扒取场地数据、竞品分析、市场调研</div>
                    </div>
                    <div class="role-card">
                        <div class="role-avatar purple"><i class="fas fa-pen-fancy"></i></div>
                        <div class="role-name">项目文案策划</div>
                        <div class="role-desc">设计说明撰写、提案文案、汇报材料</div>
                    </div>
                    <div class="role-card">
                        <div class="role-avatar green"><i class="fas fa-clipboard-check"></i></div>
                        <div class="role-name">施工落地审核员</div>
                        <div class="role-desc">规范检查、尺寸优化、动线审核</div>
                    </div>
                </div>

                <!-- 协作流程图 -->
                <div class="flow-diagram">
                    <div class="flow-step">
                        <div class="flow-icon blue"><i class="fas fa-search"></i></div>
                        <span class="flow-label">调研专员<br>收集数据</span>
                    </div>
                    <i class="fas fa-arrow-right flow-arrow"></i>
                    <div class="flow-step">
                        <div class="flow-icon purple"><i class="fas fa-lightbulb"></i></div>
                        <span class="flow-label">生成<br>设计方案</span>
                    </div>
                    <i class="fas fa-arrow-right flow-arrow"></i>
                    <div class="flow-step">
                        <div class="flow-icon orange"><i class="fas fa-paper-plane"></i></div>
                        <span class="flow-label">提交<br>审核员</span>
                    </div>
                    <i class="fas fa-arrow-right flow-arrow"></i>
                    <div class="flow-step">
                        <div class="flow-icon green"><i class="fas fa-check-double"></i></div>
                        <span class="flow-label">交叉验证<br>过滤错误</span>
                    </div>
                    <i class="fas fa-arrow-right flow-arrow"></i>
                    <div class="flow-step">
                        <div class="flow-icon blue"><i class="fas fa-clipboard-list"></i></div>
                        <span class="flow-label">输出<br>最终建议</span>
                    </div>
                </div>

                <p style="margin-top: 25px; text-align: center; color: var(--silver-gray); font-size: 0.95rem;">
                    <i class="fas fa-sync-alt" style="color: var(--accent-blue);"></i>
                    通过多 Agent 协同"开会"纠错，过滤掉不靠谱的想法，大幅提高最终给到设计师建议的准确度
                </p>
            </div>
        </div>

        <!-- 结尾 -->
        <div class="conclusion" id="conclusion">
            <div class="conclusion-icon"><i class="fas fa-handshake"></i></div>
            <p class="conclusion-text">
                目前我还在初期的学习和摸索阶段，后续如果有更成熟的稳定版本，我再向您和团队做详细演示。
            </p>
        </div>

        <!-- 底部装饰 -->
        <footer class="footer-decoration">
            <div class="footer-icons">
                <div class="footer-icon"><i class="fas fa-robot"></i></div>
                <div class="footer-icon"><i class="fas fa-leaf"></i></div>
                <div class="footer-icon"><i class="fas fa-brain"></i></div>
                <div class="footer-icon"><i class="fas fa-rocket"></i></div>
            </div>
            <p class="footer-text">AI 工具学习进程汇报 · 景观设计业务赋能探索</p>
        </footer>
    </div>

    <script>
        // 页面加载完成后隐藏加载动画
        window.addEventListener('load', function() {
            setTimeout(function() {
                document.getElementById('loadingOverlay').classList.add('hidden');
            }, 600);
        });

        // 创建粒子效果
        function createParticles() {
            const container = document.getElementById('particles');
            const particleCount = 40;

            const colors = ['#00d4ff', '#a855f7', '#3b82f6', '#10b981', '#f59e0b'];

            for (let i = 0; i < particleCount; i++) {
                const particle = document.createElement('div');
                particle.className = 'particle';
                particle.style.left = Math.random() * 100 + '%';
                particle.style.animationDuration = (Math.random() * 15 + 10) + 's';
                particle.style.animationDelay = Math.random() * 10 + 's';
                const size = Math.random() * 4 + 2;
                particle.style.width = size + 'px';
                particle.style.height = size + 'px';
                particle.style.background = colors[Math.floor(Math.random() * colors.length)];
                particle.style.boxShadow = `0 0 ${size * 2}px ${particle.style.background}`;
                container.appendChild(particle);
            }
        }
        createParticles();

        // 滚动动画
        function handleScrollAnimation() {
            const elements = [
                { el: document.getElementById('statsRow'), threshold: 0.1 },
                { el: document.getElementById('intro'), threshold: 0.1 },
                { el: document.getElementById('section1'), threshold: 0.15 },
                { el: document.getElementById('section2'), threshold: 0.15 },
                { el: document.getElementById('section3'), threshold: 0.15 },
                { el: document.getElementById('conclusion'), threshold: 0.2 }
            ];

            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add('visible');
                    }
                });
            }, {
                threshold: 0.1,
                rootMargin: '0px 0px -50px 0px'
            });

            elements.forEach(item => {
                if (item.el) observer.observe(item.el);
            });
        }
        handleScrollAnimation();
    </script>
</body>
</html>
