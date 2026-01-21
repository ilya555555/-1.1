<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Космический Кликер: Эра Восхождения</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        /* ===== ОСНОВНЫЕ СТИЛИ ===== */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary: #6c5ce7;
            --secondary: #a29bfe;
            --dark: #0f1419;
            --darker: #0a0d12;
            --light: #f5f6fa;
            --lighter: #ffffff;
            --success: #00b894;
            --success-dark: #00a085;
            --warning: #fdcb6e;
            --warning-dark: #f9a825;
            --danger: #d63031;
            --danger-dark: #c0392b;
            --info: #0984e3;
            --info-dark: #0770c4;
            --cyber-blue: #00cec9;
            --cyber-blue-dark: #00b5b0;
            --cyber-pink: #fd79a8;
            --cyber-pink-dark: #e84393;
            --space-dark: #0c2461;
            --space-darker: #07142e;
            --nebula-purple: #8e44ad;
            --nebula-purple-dark: #7d3c98;
            --star-yellow: #f1c40f;
            --star-gold: #f39c12;
            --metal-silver: #bdc3c7;
            --crystal-blue: #3498db;
            --uranium-green: #2ecc71;
            --antimatter-red: #e74c3c;
            --dark-matter: #2c3e50;
            --quantum-violet: #9b59b6;
            --galaxy-orange: #e67e22;
        }

        body {
            font-family: 'Segoe UI', 'Roboto', 'Arial', sans-serif;
            background: radial-gradient(circle at center, #0c2461 0%, #0a0d12 100%);
            color: var(--light);
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
            line-height: 1.6;
        }

        /* ===== ЗВЕЗДНЫЙ ФОН ===== */
        .stars {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: -2;
        }

        .star {
            position: absolute;
            background-color: white;
            border-radius: 50%;
            animation: twinkle var(--twinkle-duration) infinite var(--twinkle-delay);
        }

        .nebula {
            position: fixed;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle at 20% 80%, rgba(108, 92, 231, 0.1) 0%, transparent 50%),
                       radial-gradient(circle at 80% 20%, rgba(253, 121, 168, 0.1) 0%, transparent 50%),
                       radial-gradient(circle at 40% 40%, rgba(0, 206, 201, 0.05) 0%, transparent 40%);
            z-index: -1;
            pointer-events: none;
        }

        /* ===== АНИМАЦИИ ===== */
        @keyframes twinkle {
            0%, 100% { opacity: 0.2; transform: scale(1); }
            50% { opacity: 1; transform: scale(1.1); }
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-10px) rotate(2deg); }
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); box-shadow: 0 0 20px currentColor; }
            50% { transform: scale(1.05); box-shadow: 0 0 30px currentColor; }
        }

        @keyframes glow {
            0%, 100% { filter: brightness(1); }
            50% { filter: brightness(1.3); }
        }

        @keyframes rotate {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            75% { transform: translateX(5px); }
        }

        @keyframes particle-trail {
            0% { transform: translate(0, 0) scale(1); opacity: 1; }
            100% { transform: translate(var(--tx), var(--ty)) scale(0); opacity: 0; }
        }

        /* ===== ОСНОВНОЙ КОНТЕЙНЕР ===== */
        .container {
            max-width: 1800px;
            margin: 0 auto;
            padding: 20px;
            display: grid;
            grid-template-columns: 1fr 350px;
            gap: 25px;
            min-height: 100vh;
        }

        /* ===== ШАПКА ===== */
        .header {
            grid-column: 1 / -1;
            background: linear-gradient(135deg, rgba(44, 62, 80, 0.95), rgba(30, 39, 46, 0.95));
            padding: 25px 35px;
            border-radius: 20px;
            margin-bottom: 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border: 3px solid var(--cyber-blue);
            box-shadow: 0 0 40px rgba(0, 206, 201, 0.4),
                        0 10px 30px rgba(0, 0, 0, 0.3);
            position: relative;
            overflow: hidden;
        }

        .header::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(0, 206, 201, 0.1), transparent);
            animation: header-glow 3s infinite;
        }

        @keyframes header-glow {
            100% { left: 100%; }
        }

        .game-title {
            font-size: 3.2rem;
            background: linear-gradient(45deg, var(--cyber-blue), var(--cyber-pink), var(--nebula-purple));
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: 0 0 30px rgba(0, 206, 201, 0.7);
            font-weight: 900;
            letter-spacing: 1px;
            position: relative;
            display: flex;
            align-items: center;
            gap: 20px;
        }

        .game-title i {
            animation: float 3s ease-in-out infinite;
            text-shadow: 0 0 20px currentColor;
        }

        .stats-bar {
            display: flex;
            gap: 40px;
            background: rgba(0, 0, 0, 0.4);
            padding: 15px 25px;
            border-radius: 15px;
            border: 2px solid rgba(255, 255, 255, 0.1);
        }

        .stat-item {
            text-align: center;
            min-width: 120px;
            position: relative;
        }

        .stat-item::after {
            content: '';
            position: absolute;
            right: -20px;
            top: 50%;
            transform: translateY(-50%);
            width: 1px;
            height: 40px;
            background: linear-gradient(to bottom, transparent, var(--cyber-blue), transparent);
        }

        .stat-item:last-child::after {
            display: none;
        }

        .stat-label {
            font-size: 0.9rem;
            color: var(--secondary);
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 5px;
        }

        .stat-value {
            font-size: 2.4rem;
            font-weight: 800;
            color: var(--warning);
            text-shadow: 0 0 15px rgba(253, 203, 110, 0.7);
            font-family: 'Courier New', monospace;
            animation: glow 2s infinite;
        }

        /* ===== ОСНОВНАЯ ИГРОВАЯ ОБЛАСТЬ ===== */
        .main-game {
            display: grid;
            grid-template-columns: 1fr 400px;
            gap: 25px;
        }

        /* Кликер секция */
        .clicker-section {
            background: linear-gradient(145deg, rgba(30, 39, 46, 0.95), rgba(44, 62, 80, 0.95));
            border-radius: 25px;
            padding: 35px;
            text-align: center;
            border: 3px solid var(--primary);
            position: relative;
            overflow: hidden;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.4);
            transition: all 0.3s;
        }

        .clicker-section:hover {
            border-color: var(--cyber-blue);
            box-shadow: 0 20px 40px rgba(0, 206, 201, 0.3);
        }

        .clicker-title {
            font-size: 2.2rem;
            margin-bottom: 25px;
            color: var(--secondary);
            text-shadow: 0 0 15px rgba(162, 155, 254, 0.5);
            position: relative;
            display: inline-block;
        }

        .clicker-title::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 25%;
            width: 50%;
            height: 3px;
            background: linear-gradient(90deg, transparent, var(--cyber-blue), transparent);
        }

        .click-button-container {
            position: relative;
            margin: 30px auto;
            width: 320px;
            height: 320px;
            perspective: 1000px;
        }

        .click-button {
            width: 100%;
            height: 100%;
            border-radius: 50%;
            background: radial-gradient(circle at 30% 30%, var(--primary), var(--space-dark));
            border: 6px solid var(--cyber-pink);
            color: white;
            font-size: 1.8rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.15s;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            box-shadow: 0 0 50px rgba(253, 121, 168, 0.5),
                        inset 0 0 40px rgba(255, 255, 255, 0.1),
                        0 0 0 10px rgba(108, 92, 231, 0.3);
            position: relative;
            overflow: hidden;
            transform-style: preserve-3d;
            animation: float 4s ease-in-out infinite;
        }

        .click-button::before {
            content: '';
            position: absolute;
            top: -10px;
            left: -10px;
            right: -10px;
            bottom: -10px;
            background: linear-gradient(45deg, transparent 30%, rgba(255, 255, 255, 0.1) 50%, transparent 70%);
            border-radius: 50%;
            animation: rotate 20s linear infinite;
            z-index: 1;
        }

        .click-button:hover {
            transform: scale(1.08) rotate(5deg);
            box-shadow: 0 0 70px rgba(253, 121, 168, 0.7);
        }

        .click-button:active {
            transform: scale(0.95);
            box-shadow: 0 0 100px rgba(253, 121, 168, 0.9);
        }

        .click-button i {
            font-size: 5.5rem;
            margin-bottom: 15px;
            text-shadow: 0 0 30px currentColor;
            position: relative;
            z-index: 2;
        }

        .click-button .click-power {
            font-size: 1.4rem;
            color: var(--warning);
            text-shadow: 0 0 10px rgba(253, 203, 110, 0.8);
            margin-top: 10px;
            position: relative;
            z-index: 2;
        }

        .click-button .click-multiplier {
            position: absolute;
            font-size: 3.5rem;
            font-weight: bold;
            color: var(--star-yellow);
            text-shadow: 0 0 20px rgba(241, 196, 15, 0.9);
            opacity: 0;
            pointer-events: none;
            z-index: 10;
            animation: floatUp 1.2s ease-out forwards;
        }

        @keyframes floatUp {
            0% { opacity: 1; transform: translate(-50%, -50%) scale(1); }
            100% { opacity: 0; transform: translate(-50%, -150px) scale(1.8); }
        }

        /* Частицы при клике */
        .click-particle {
            position: absolute;
            width: 10px;
            height: 10px;
            background: var(--cyber-pink);
            border-radius: 50%;
            pointer-events: none;
            z-index: 5;
            animation: particle-trail 0.8s ease-out forwards;
        }

        /* ===== СЕКЦИЯ УЛУЧШЕНИЙ ===== */
        .upgrades-section {
            background: linear-gradient(145deg, rgba(30, 39, 46, 0.95), rgba(44, 62, 80, 0.95));
            border-radius: 25px;
            padding: 25px;
            border: 3px solid var(--success);
            max-height: 700px;
            overflow-y: auto;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.4);
            position: relative;
        }

        .upgrades-section::-webkit-scrollbar {
            width: 12px;
        }

        .upgrades-section::-webkit-scrollbar-track {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 6px;
        }

        .upgrades-section::-webkit-scrollbar-thumb {
            background: linear-gradient(to bottom, var(--cyber-blue), var(--primary));
            border-radius: 6px;
            border: 2px solid rgba(0, 0, 0, 0.3);
        }

        .section-title {
            font-size: 1.8rem;
            margin-bottom: 20px;
            color: var(--cyber-blue);
            border-bottom: 3px solid var(--cyber-blue);
            padding-bottom: 10px;
            text-shadow: 0 0 15px rgba(0, 206, 201, 0.5);
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .section-title i {
            animation: pulse 2s infinite;
        }

        .upgrade-category {
            margin-bottom: 25px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 15px;
            padding: 15px;
            border: 2px solid rgba(255, 255, 255, 0.05);
        }

        .category-title {
            font-size: 1.4rem;
            color: var(--warning);
            margin-bottom: 15px;
            padding-left: 10px;
            border-left: 4px solid var(--warning);
            text-shadow: 0 0 10px rgba(253, 203, 110, 0.5);
        }

        .upgrade-item {
            background: linear-gradient(135deg, rgba(52, 73, 94, 0.8), rgba(44, 62, 80, 0.8));
            border-radius: 12px;
            padding: 18px;
            margin-bottom: 12px;
            border: 2px solid rgba(255, 255, 255, 0.1);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            cursor: pointer;
            position: relative;
            overflow: hidden;
        }

        .upgrade-item::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
            transition: left 0.6s;
        }

        .upgrade-item:hover::before {
            left: 100%;
        }

        .upgrade-item:hover {
            background: linear-gradient(135deg, rgba(72, 93, 114, 0.9), rgba(64, 82, 100, 0.9));
            transform: translateX(8px) scale(1.02);
            border-color: var(--info);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
        }

        .upgrade-item.purchased {
            background: linear-gradient(135deg, rgba(46, 204, 113, 0.3), rgba(39, 174, 96, 0.2));
            border-color: var(--success);
        }

        .upgrade-item.max-level {
            background: linear-gradient(135deg, rgba(155, 89, 182, 0.3), rgba(142, 68, 173, 0.2));
            border-color: var(--quantum-violet);
        }

        .upgrade-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }

        .upgrade-name {
            font-weight: 700;
            color: var(--light);
            font-size: 1.2rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .upgrade-cost {
            color: var(--warning);
            font-weight: 800;
            font-size: 1.3rem;
            font-family: 'Courier New', monospace;
            text-shadow: 0 0 10px rgba(253, 203, 110, 0.7);
        }

        .upgrade-description {
            font-size: 1rem;
            color: #bdc3c7;
            margin-bottom: 10px;
            line-height: 1.5;
        }

        .upgrade-effect {
            font-size: 0.95rem;
            color: var(--info);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .upgrade-level {
            color: var(--cyber-pink);
            font-weight: bold;
        }

        .upgrade-progress {
            height: 6px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 3px;
            margin-top: 8px;
            overflow: hidden;
        }

        .upgrade-progress-bar {
            height: 100%;
            background: linear-gradient(90deg, var(--cyber-blue), var(--cyber-pink));
            width: 0%;
            transition: width 0.5s ease;
            border-radius: 3px;
        }

        /* ===== БОКОВАЯ ПАНЕЛЬ ===== */
        .sidebar {
            display: flex;
            flex-direction: column;
            gap: 25px;
        }

        /* Общие стили для всех секций */
        .resources-section,
        .automation-section,
        .prestige-section,
        .research-section,
        .quests-section,
        .achievements-section,
        .events-section,
        .multipliers-section,
        .save-section,
        .crafting-section,
        .galaxy-section,
        .combat-section,
        .prestige-shop-section,
        .skill-tree-section,
        .market-section,
        .leaderboard-section,
        .daily-rewards-section {
            background: linear-gradient(145deg, rgba(30, 39, 46, 0.95), rgba(44, 62, 80, 0.95));
            border-radius: 25px;
            padding: 25px;
            border: 3px solid var(--cyber-blue);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.4);
            transition: all 0.3s;
        }

        .resources-section { border-color: var(--metal-silver); }
        .automation-section { border-color: var(--success); }
        .prestige-section { border-color: var(--star-gold); }
        .research-section { border-color: var(--info); }
        .quests-section { border-color: var(--galaxy-orange); }
        .achievements-section { border-color: var(--warning); }
        .events-section { border-color: var(--cyber-pink); }
        .multipliers-section { border-color: var(--nebula-purple); }
        .crafting-section { border-color: var(--crystal-blue); }
        .galaxy-section { border-color: var(--uranium-green); }
        .combat-section { border-color: var(--danger); }
        .prestige-shop-section { border-color: var(--quantum-violet); }
        .skill-tree-section { border-color: var(--cyber-blue); }
        .market-section { border-color: var(--success); }
        .leaderboard-section { border-color: var(--warning); }
        .daily-rewards-section { border-color: var(--info); }

        /* Секция ресурсов */
        .resource-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
            gap: 15px;
        }

        .resource-item {
            background: rgba(41, 128, 185, 0.2);
            border-radius: 12px;
            padding: 20px;
            text-align: center;
            border: 2px solid rgba(52, 152, 219, 0.3);
            transition: all 0.3s;
            position: relative;
            overflow: hidden;
        }

        .resource-item:hover {
            transform: translateY(-5px);
            border-color: var(--info);
            box-shadow: 0 10px 20px rgba(52, 152, 219, 0.2);
        }

        .resource-icon {
            font-size: 2.8rem;
            margin-bottom: 15px;
            color: var(--cyber-blue);
            text-shadow: 0 0 20px currentColor;
            animation: float 3s ease-in-out infinite;
        }

        .resource-name {
            font-weight: 700;
            color: var(--light);
            font-size: 1.1rem;
            margin-bottom: 5px;
        }

        .resource-value {
            font-size: 1.8rem;
            font-weight: 800;
            color: var(--warning);
            font-family: 'Courier New', monospace;
        }

        .resource-per-second {
            font-size: 0.9rem;
            color: var(--success);
            margin-top: 5px;
        }

        /* Секция достижений */
        .achievements-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 15px;
        }

        .achievement {
            background: rgba(243, 156, 18, 0.15);
            border-radius: 12px;
            padding: 20px;
            border: 2px solid rgba(243, 156, 18, 0.3);
            transition: all 0.3s;
            position: relative;
            overflow: hidden;
        }

        .achievement.unlocked {
            background: rgba(243, 156, 18, 0.3);
            border-color: var(--warning);
            box-shadow: 0 0 20px rgba(243, 156, 18, 0.3);
        }

        .achievement:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 30px rgba(243, 156, 18, 0.2);
        }

        .achievement-icon {
            font-size: 2.5rem;
            margin-bottom: 15px;
            text-align: center;
        }

        .achievement-name {
            font-weight: 700;
            color: var(--light);
            font-size: 1.2rem;
            margin-bottom: 8px;
            text-align: center;
        }

        .achievement-description {
            font-size: 0.95rem;
            color: #bdc3c7;
            margin-bottom: 10px;
            text-align: center;
        }

        .achievement-progress {
            height: 8px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 4px;
            margin-top: 10px;
            overflow: hidden;
        }

        .achievement-progress-bar {
            height: 100%;
            background: linear-gradient(90deg, var(--warning), var(--star-gold));
            border-radius: 4px;
            width: 0%;
            transition: width 0.5s ease;
        }

        /* Кнопки */
        .btn {
            background: linear-gradient(135deg, var(--primary), var(--nebula-purple));
            color: white;
            border: none;
            padding: 15px 25px;
            border-radius: 12px;
            font-size: 1.1rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            width: 100%;
            margin-bottom: 12px;
            text-transform: uppercase;
            letter-spacing: 1px;
            position: relative;
            overflow: hidden;
        }

        .btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transition: left 0.6s;
        }

        .btn:hover::before {
            left: 100%;
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(108, 92, 231, 0.4);
        }

        .btn:active {
            transform: translateY(1px);
        }

        .btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none !important;
        }

        .btn-success {
            background: linear-gradient(135deg, var(--success), var(--success-dark));
        }

        .btn-warning {
            background: linear-gradient(135deg, var(--warning), var(--warning-dark));
        }

        .btn-danger {
            background: linear-gradient(135deg, var(--danger), var(--danger-dark));
        }

        .btn-info {
            background: linear-gradient(135deg, var(--info), var(--info-dark));
        }

        /* Уведомления */
        .notification-container {
            position: fixed;
            bottom: 30px;
            right: 30px;
            width: 400px;
            z-index: 10000;
            display: flex;
            flex-direction: column;
            gap: 15px;
            pointer-events: none;
        }

        .notification {
            background: linear-gradient(135deg, rgba(44, 62, 80, 0.95), rgba(30, 39, 46, 0.95));
            border-left: 6px solid var(--success);
            padding: 20px 25px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.4);
            transform: translateX(500px);
            transition: transform 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55);
            pointer-events: auto;
            backdrop-filter: blur(10px);
            border: 2px solid rgba(255, 255, 255, 0.1);
        }

        .notification.show {
            transform: translateX(0);
        }

        .notification.warning { border-color: var(--warning); }
        .notification.error { border-color: var(--danger); }
        .notification.info { border-color: var(--info); }
        .notification.prestige { border-color: var(--star-gold); }

        .notification-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }

        .notification-title {
            font-weight: 700;
            color: var(--light);
            font-size: 1.2rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .notification-close {
            background: none;
            border: none;
            color: var(--light);
            cursor: pointer;
            font-size: 1.2rem;
            opacity: 0.7;
            transition: opacity 0.3s;
        }

        .notification-close:hover {
            opacity: 1;
        }

        .notification-content {
            color: #bdc3c7;
            line-height: 1.5;
        }

        /* Прогресс бар */
        .progress-bar {
            height: 20px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 10px;
            overflow: hidden;
            margin: 15px 0;
            position: relative;
            border: 2px solid rgba(255, 255, 255, 0.1);
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--cyber-blue), var(--cyber-pink));
            border-radius: 8px;
            width: 0%;
            transition: width 0.5s ease;
            position: relative;
            overflow: hidden;
        }

        .progress-fill::after {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            animation: progress-shimmer 2s infinite;
        }

        @keyframes progress-shimmer {
            100% { left: 100%; }
        }

        .progress-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: white;
            font-weight: 700;
            text-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
            font-size: 0.9rem;
        }

        /* Модальные окна */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            z-index: 100000;
            justify-content: center;
            align-items: center;
            backdrop-filter: blur(5px);
        }

        .modal.show {
            display: flex;
            animation: modal-fade 0.3s ease;
        }

        @keyframes modal-fade {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .modal-content {
            background: linear-gradient(145deg, var(--dark), var(--darker));
            border-radius: 25px;
            padding: 40px;
            max-width: 800px;
            width: 90%;
            max-height: 90vh;
            overflow-y: auto;
            border: 3px solid var(--cyber-blue);
            box-shadow: 0 0 100px rgba(0, 206, 201, 0.5);
            position: relative;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
        }

        .modal-title {
            font-size: 2.5rem;
            color: var(--cyber-blue);
            text-shadow: 0 0 20px rgba(0, 206, 201, 0.7);
            font-weight: 900;
        }

        .modal-close {
            background: none;
            border: none;
            color: var(--light);
            font-size: 2rem;
            cursor: pointer;
            transition: color 0.3s;
        }

        .modal-close:hover {
            color: var(--danger);
        }

        /* Адаптивность */
        @media (max-width: 1600px) {
            .container {
                grid-template-columns: 1fr;
            }
            
            .main-game {
                grid-template-columns: 1fr;
            }
            
            .sidebar {
                grid-column: 1;
                display: grid;
                grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
                gap: 25px;
            }
        }

        @media (max-width: 1200px) {
            .header {
                flex-direction: column;
                gap: 25px;
                text-align: center;
            }
            
            .stats-bar {
                flex-wrap: wrap;
                justify-content: center;
            }
            
            .stat-item::after {
                display: none;
            }
            
            .click-button-container {
                width: 280px;
                height: 280px;
            }
        }

        @media (max-width: 768px) {
            .container {
                padding: 15px;
                gap: 15px;
            }
            
            .game-title {
                font-size: 2.2rem;
            }
            
            .stat-value {
                font-size: 1.8rem;
            }
            
            .click-button-container {
                width: 250px;
                height: 250px;
            }
            
            .click-button i {
                font-size: 4rem;
            }
            
            .section-title {
                font-size: 1.5rem;
            }
            
            .notification-container {
                width: calc(100% - 30px);
                right: 15px;
            }
        }

        /* Анимация загрузки */
        .loading-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--darker);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 1000000;
            transition: opacity 0.5s ease;
        }

        .loading-spinner {
            width: 80px;
            height: 80px;
            border: 6px solid rgba(0, 206, 201, 0.3);
            border-top-color: var(--cyber-blue);
            border-radius: 50%;
            animation: rotate 1s linear infinite;
            margin-bottom: 30px;
        }

        .loading-text {
            font-size: 1.8rem;
            color: var(--cyber-blue);
            text-shadow: 0 0 20px rgba(0, 206, 201, 0.7);
            font-weight: 700;
            letter-spacing: 2px;
        }

        /* Табы */
        .tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 25px;
            flex-wrap: wrap;
            border-bottom: 2px solid rgba(255, 255, 255, 0.1);
            padding-bottom: 15px;
        }

        .tab {
            background: rgba(255, 255, 255, 0.1);
            border: none;
            color: var(--light);
            padding: 12px 25px;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s;
            font-weight: 600;
            position: relative;
            overflow: hidden;
        }

        .tab:hover {
            background: rgba(255, 255, 255, 0.2);
            transform: translateY(-2px);
        }

        .tab.active {
            background: var(--cyber-blue);
            color: var(--dark);
            box-shadow: 0 5px 15px rgba(0, 206, 201, 0.4);
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
            animation: tab-fade 0.3s ease;
        }

        @keyframes tab-fade {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Иконка уведомления на вкладке */
        .tab-notification {
            position: absolute;
            top: -5px;
            right: -5px;
            width: 20px;
            height: 20px;
            background: var(--danger);
            border-radius: 50%;
            color: white;
            font-size: 0.7rem;
            display: flex;
            align-items: center;
            justify-content: center;
            animation: pulse 1s infinite;
        }

        /* Стили для дерева исследований */
        .research-node {
            background: rgba(52, 152, 219, 0.2);
            border: 2px solid var(--info);
            border-radius: 12px;
            padding: 20px;
            text-align: center;
            transition: all 0.3s;
            cursor: pointer;
            position: relative;
        }

        .research-node:hover {
            transform: scale(1.05);
            box-shadow: 0 0 30px rgba(52, 152, 219, 0.3);
        }

        .research-node.unlocked {
            background: rgba(46, 204, 113, 0.3);
            border-color: var(--success);
        }

        .research-node.locked {
            background: rgba(189, 195, 199, 0.2);
            border-color: var(--metal-silver);
            opacity: 0.5;
            cursor: not-allowed;
        }

        .research-connection {
            position: absolute;
            background: var(--info);
            height: 3px;
            transform-origin: left center;
        } 
    </style>
</head>
<body>
    <!-- Экран загрузки -->
    <div class="loading-screen" id="loadingScreen">
        <div class="loading-spinner"></div>
        <div class="loading-text">ЗАГРУЗКА КОСМИЧЕСКОГО КЛИКЕРА...</div>
        <div style="margin-top: 20px; color: var(--secondary); text-align: center;">
            <div>Версия 2.0.0</div>
            <div style="font-size: 0.9rem; margin-top: 10px;">Подготовка галактических систем...</div>
        </div>
    </div>

    <!-- Звездный фон -->
    <div class="stars" id="stars"></div>
    <div class="nebula"></div>

    <!-- Контейнер уведомлений -->
    <div class="notification-container" id="notificationContainer"></div>

    <!-- Модальное окно престижа -->
    <div class="modal" id="prestigeModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title"><i class="fas fa-star"></i> ПРЕСТИЖ</h2>
                <button class="modal-close" id="closePrestigeModal"><i class="fas fa-times"></i></button>
            </div>
            <div id="prestigeModalContent">
                <!-- Контент будет заполнен через JavaScript -->
            </div>
        </div>
    </div>

    <!-- Модальное окно галактики -->
    <div class="modal" id="galaxyModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title"><i class="fas fa-globe"></i> ГАЛАКТИЧЕСКАЯ КАРТА</h2>
                <button class="modal-close" id="closeGalaxyModal"><i class="fas fa-times"></i></button>
            </div>
            <div id="galaxyModalContent">
                <!-- Контент будет заполнен через JavaScript -->
            </div>
        </div>
    </div>

    <div class="container">
        <!-- Шапка -->
        <div class="header">
            <h1 class="game-title">
                <i class="fas fa-rocket"></i> Космический Кликер: Эра Восхождения
            </h1>
            <div class="stats-bar">
                <div class="stat-item">
                    <div class="stat-label">Энергия</div>
                    <div class="stat-value" id="energy">0</div>
                </div>
                <div class="stat-item">
                    <div class="stat-label">ЭПС</div>
                    <div class="stat-value" id="eps">0</div>
                </div>
                <div class="stat-item">
                    <div class="stat-label">Уровень</div>
                    <div class="stat-value" id="level">1</div>
                </div>
                <div class="stat-item">
                    <div class="stat-label">Престиж</div>
                    <div class="stat-value" id="prestige">0</div>
                </div>
                <div class="stat-item">
                    <div class="stat-label">Мульти</div>
                    <div class="stat-value" id="multiplier">1x</div>
                </div>
            </div>
        </div>

        <!-- Основная игровая область -->
        <div class="main-game">
            <div>
                <!-- Кликер -->
                <div class="clicker-section">
                    <h2 class="clicker-title">Генератор Сингулярности</h2>
                    <div class="click-button-container">
                        <button class="click-button" id="clickButton">
                            <i class="fas fa-bolt"></i>
                            <span>ВЫСВОБОДИТЬ ЭНЕРГИЮ</span>
                            <div class="click-power" id="clickPower">+1 за клик</div>
                        </button>
                    </div>
                    <div class="progress-bar">
                        <div class="progress-fill" id="levelProgress"></div>
                        <div class="progress-text" id="levelProgressText">0%</div>
                    </div>
                    <p style="margin-top: 20px; color: var(--secondary); font-size: 1.1rem;">
                        Кликайте для генерации энергии квантового синтеза. Улучшайте мощность и открывайте новые технологии!
                    </p>
                </div>

                <!-- Ресурсы -->
                <div class="resources-section">
                    <h3 class="section-title"><i class="fas fa-gem"></i> Галактические Ресурсы</h3>
                    <div class="tabs" id="resourceTabs">
                        <button class="tab active" data-tab="basic">Основные</button>
                        <button class="tab" data-tab="advanced">Продвинутые</button>
                        <button class="tab" data-tab="exotic">Экзотические</button>
                    </div>
                    <div class="tab-content active" id="basicResources">
                        <div class="resource-grid" id="resourcesGrid">
                            <!-- Ресурсы будут добавлены через JavaScript -->
                        </div>
                    </div>
                    <div class="tab-content" id="advancedResources">
                        <!-- Продвинутые ресурсы будут добавлены через JavaScript -->
                    </div>
                    <div class="tab-content" id="exoticResources">
                        <!-- Экзотические ресурсы будут добавлены через JavaScript -->
                    </div>
                </div>

                <!-- Автоматизация -->
                <div class="automation-section">
                    <h3 class="section-title"><i class="fas fa-robot"></i> Автоматизированные Системы</h3>
                    <div id="automationGrid">
                        <!-- Автоматизация будет добавлена через JavaScript -->
                    </div>
                </div>
            </div>

            <!-- Улучшения -->
            <div class="upgrades-section">
                <h3 class="section-title"><i class="fas fa-arrow-up"></i> ИмпЕРИАЛЬНЫЕ УЛУЧШЕНИЯ</h3>
                <div class="tabs" id="upgradeTabs">
                    <button class="tab active" data-tab="click">Клики</button>
                    <button class="tab" data-tab="production">Производство</button>
                    <button class="tab" data-tab="multiplier">Мультипликаторы</button>
                    <button class="tab" data-tab="special">Особые</button>
                </div>
                <div id="upgradesList">
                    <!-- Улучшения будут добавлены через JavaScript -->
                </div>
            </div>
        </div>

        <!-- Боковая панель -->
        <div class="sidebar">
            <!-- Достижения -->
            <div class="achievements-section">
                <h3 class="section-title"><i class="fas fa-trophy"></i> Галактические Достижения</h3>
                <div class="tabs">
                    <button class="tab active" data-tab="achievements">Достижения</button>
                    <button class="tab" data-tab="milestones">Вершины</button>
                </div>
                <div class="achievements-grid" id="achievementsGrid">
                    <!-- Достижения будут добавлены через JavaScript -->
                </div>
            </div>

            <!-- Исследования -->
            <div class="research-section">
                <h3 class="section-title"><i class="fas fa-flask"></i> Исследования</h3>
                <div id="researchTree">
                    <!-- Дерево исследований будет добавлено через JavaScript -->
                </div>
            </div>

            <!-- Престиж -->
            <div class="prestige-section">
                <h3 class="section-title"><i class="fas fa-star"></i> Система Престижа</h3>
                <div style="margin-bottom: 20px;">
                    <div style="display: flex; justify-content: space-between; margin-bottom: 10px;">
                        <span>Текущие очки престижа:</span>
                        <span class="stat-value" style="font-size: 1.5rem;" id="prestigePoints">0</span>
                    </div>
                    <div style="display: flex; justify-content: space-between; margin-bottom: 20px;">
                        <span>Мультипликатор:</span>
                        <span class="stat-value" style="font-size: 1.5rem;" id="prestigeMultiplier">1x</span>
                    </div>
                    <button class="btn btn-warning" id="prestigeButton">
                        <i class="fas fa-redo"></i> ПРЕСТИЖ
                    </button>
                    <button class="btn btn-info" id="prestigeShopButton">
                        <i class="fas fa-shopping-cart"></i> Магазин Престижа
                    </button>
                </div>
            </div>

            <!-- Крафтинг -->
            <div class="crafting-section">
                <h3 class="section-title"><i class="fas fa-hammer"></i> Космический Крафтинг</h3>
                <div id="craftingRecipes">
                    <!-- Рецепты будут добавлены через JavaScript -->
                </div>
            </div>

            <!-- События -->
            <div class="events-section">
                <h3 class="section-title"><i class="fas fa-bolt"></i> Космические События</h3>
                <div id="currentEvents">
                    <!-- Текущие события будут добавлены через JavaScript -->
                </div>
            </div>

            <!-- Сохранение/Загрузка -->
            <div class="save-section">
                <h3 class="section-title"><i class="fas fa-save"></i> Система Сохранения</h3>
                <button class="btn btn-success" id="saveButton">
                    <i class="fas fa-save"></i> Сохранить Игру
                </button>
                <button class="btn btn-info" id="loadButton">
                    <i class="fas fa-folder-open"></i> Загрузить Игру
                </button>
                <button class="btn btn-danger" id="resetButton">
                    <i class="fas fa-skull-crossbones"></i> Сбросить Игру
                </button>
                <button class="btn" id="exportButton" style="background: linear-gradient(135deg, var(--quantum-violet), var(--nebula-purple));">
                    <i class="fas fa-file-export"></i> Экспорт
                </button>
                <button class="btn" id="importButton" style="background: linear-gradient(135deg, var(--galaxy-orange), var(--warning));">
                    <i class="fas fa-file-import"></i> Импорт
                </button>
            </div>
        </div>
    </div>
<script>
        // ===== КОНФИГУРАЦИЯ ИГРЫ =====
        const CONFIG = {
            VERSION: "2.0.0",
            SAVE_KEY: "spaceClickerExtendedSave",
            AUTOSAVE_INTERVAL: 30000,
            TICK_INTERVAL: 1000,
            OFFLINE_MAX_TIME: 86400,
            NOTIFICATION_DURATION: 5000,
            CLICK_COOLDOWN: 50
        };

        // ===== КЛАСС РЕСУРСА =====
        class Resource {
            constructor(id, name, icon, color, description = "", perSecond = 0, max = Infinity, unlockRequirement = null) {
                this.id = id;
                this.name = name;
                this.icon = icon;
                this.color = color;
                this.description = description;
                this.value = 0;
                this.total = 0;
                this.perSecond = perSecond;
                this.max = max;
                this.unlocked = unlockRequirement === null;
                this.unlockRequirement = unlockRequirement;
                this.upgrades = [];
            }

            add(amount) {
                const oldValue = this.value;
                this.value = Math.min(this.value + amount, this.max);
                this.total += Math.max(0, this.value - oldValue);
                return this.value - oldValue;
            }

            subtract(amount) {
                if (this.value >= amount) {
                    this.value -= amount;
                    return true;
                }
                return false;
            }

            produce(deltaTime) {
                if (this.perSecond > 0 && this.unlocked) {
                    const produced = (this.perSecond * deltaTime) / 1000;
                    this.add(produced);
                    return produced;
                }
                return 0;
            }

            formatValue() {
                return formatNumber(this.value);
            }

            formatTotal() {
                return formatNumber(this.total);
            }

            formatPerSecond() {
                return formatNumber(this.perSecond) + "/сек";
            }
        }

        // ===== КЛАСС УЛУЧШЕНИЯ =====
        class Upgrade {
            constructor(id, name, description, cost, category, effect, maxLevel = 1, scaling = 1.15, unlockRequirement = null) {
                this.id = id;
                this.name = name;
                this.description = description;
                this.baseCost = cost;
                this.cost = cost;
                this.category = category;
                this.effect = effect;
                this.level = 0;
                this.maxLevel = maxLevel;
                this.scaling = scaling;
                this.unlocked = unlockRequirement === null;
                this.unlockRequirement = unlockRequirement;
                this.purchased = false;
            }

            getEffectValue() {
                if (typeof this.effect.value === 'function') {
                    return this.effect.value(this.level);
                }
                return this.effect.value * (this.level || 1);
            }

            getNextCost() {
                if (this.level >= this.maxLevel) return Infinity;
                return Math.floor(this.baseCost * Math.pow(this.scaling, this.level));
            }

            canPurchase(resources) {
                if (this.level >= this.maxLevel) return false;
                if (!this.unlocked) return false;
                return resources.energy.value >= this.getNextCost();
            }

            purchase() {
                if (this.level < this.maxLevel) {
                    this.level++;
                    this.cost = this.getNextCost();
                    this.purchased = true;
                    return true;
                }
                return false;
            }

            isMaxLevel() {
                return this.level >= this.maxLevel;
            }
        }

        // ===== КЛАСС АВТОМАТИЗАЦИИ =====
        class Automation {
            constructor(id, name, description, cost, production, resourceId, unlockRequirement = null) {
                this.id = id;
                this.name = name;
                this.description = description;
                this.cost = cost;
                this.production = production;
                this.resourceId = resourceId;
                this.count = 0;
                this.unlocked = unlockRequirement === null;
                this.unlockRequirement = unlockRequirement;
                this.efficiency = 1;
            }

            getTotalProduction() {
                return this.count * this.production * this.efficiency;
            }

            canPurchase(resources) {
                if (!this.unlocked) return false;
                return resources.energy.value >= this.cost;
            }

            purchase(resources) {
                if (resources.energy.subtract(this.cost)) {
                    this.count++;
                    this.cost = Math.floor(this.cost * 1.15);
                    return true;
                }
                return false;
            }
        }

        // ===== КЛАСС ДОСТИЖЕНИЯ =====
        class Achievement {
            constructor(id, name, description, condition, reward, icon = "fas fa-trophy", tier = 1) {
                this.id = id;
                this.name = name;
                this.description = description;
                this.condition = condition;
                this.reward = reward;
                this.icon = icon;
                this.tier = tier;
                this.unlocked = false;
                this.progress = 0;
                this.maxProgress = 1;
            }

            check(game) {
                if (this.unlocked) return false;
                
                const result = this.condition(game);
                if (typeof result === 'object') {
                    this.progress = result.progress;
                    this.maxProgress = result.max;
                    if (this.progress >= this.maxProgress) {
                        this.unlock(game);
                        return true;
                    }
                } else if (result === true) {
                    this.unlock(game);
                    return true;
                }
                return false;
            }

            unlock(game) {
                if (this.unlocked) return;
                this.unlocked = true;
                this.progress = this.maxProgress;
                
                // Применяем награду
                if (this.reward) {
                    this.reward(game);
                }
                
                return true;
            }

            getProgressPercent() {
                return Math.min(100, (this.progress / this.maxProgress) * 100);
            }
        }

        // ===== КЛАСС ИССЛЕДОВАНИЯ =====
        class Research {
            constructor(id, name, description, cost, time, requirements, effect, icon = "fas fa-flask", tier = 1) {
                this.id = id;
                this.name = name;
                this.description = description;
                this.cost = cost;
                this.time = time;
                this.requirements = requirements;
                this.effect = effect;
                this.icon = icon;
                this.tier = tier;
                this.unlocked = false;
                this.completed = false;
                this.inProgress = false;
                this.progress = 0;
                this.researchers = 0;
            }

            canStart(game) {
                if (this.completed || this.inProgress) return false;
                if (!this.requirements.every(req => req(game))) return false;
                return game.resources.science.value >= this.cost;
            }

            start(game) {
                if (this.canStart(game)) {
                    game.resources.science.subtract(this.cost);
                    this.inProgress = true;
                    this.progress = 0;
                    return true;
                }
                return false;
            }

            update(deltaTime) {
                if (this.inProgress && !this.completed) {
                    this.progress += (deltaTime / 1000) * (1 + this.researchers * 0.5);
                    if (this.progress >= this.time) {
                        this.complete();
                        return true;
                    }
                }
                return false;
            }

            complete() {
                this.inProgress = false;
                this.completed = true;
                this.progress = this.time;
                
                // Применяем эффект
                if (this.effect) {
                    this.effect(game);
                }
                
                return true;
            }

            getProgressPercent() {
                return Math.min(100, (this.progress / this.time) * 100);
            }
        }

        // ===== КЛАСС КВЕСТА =====
        class Quest {
            constructor(id, name, description, objectives, rewards, timeLimit = null, repeatable = false) {
                this.id = id;
                this.name = name;
                this.description = description;
                this.objectives = objectives;
                this.rewards = rewards;
                this.timeLimit = timeLimit;
                this.repeatable = repeatable;
                this.accepted = false;
                this.completed = false;
                this.progress = {};
                this.startTime = null;
                this.completionTime = null;
            }

            accept() {
                if (!this.accepted && !this.completed) {
                    this.accepted = true;
                    this.startTime = Date.now();
                    this.progress = Object.fromEntries(this.objectives.map(obj => [obj.id, 0]));
                    return true;
                }
                return false;
            }

            update(game) {
                if (!this.accepted || this.completed) return false;
                
                let allComplete = true;
                for (const objective of this.objectives) {
                    if (this.progress[objective.id] < objective.target) {
                        const newProgress = objective.check(game);
                        this.progress[objective.id] = newProgress;
                        if (newProgress < objective.target) {
                            allComplete = false;
                        }
                    }
                }
                
                if (allComplete) {
                    this.complete(game);
                    return true;
                }
                
                // Проверка времени
                if (this.timeLimit && Date.now() - this.startTime > this.timeLimit) {
                    this.fail();
                    return false;
                }
                
                return false;
            }

            complete(game) {
                if (this.accepted && !this.completed) {
                    this.completed = true;
                    this.completionTime = Date.now();
                    
                    // Выдаем награды
                    for (const reward of this.rewards) {
                        reward(game);
                    }
                    
                    return true;
                }
                return false;
            }

            fail() {
                this.accepted = false;
                this.progress = {};
                this.startTime = null;
                return true;
            }

            getProgressPercent() {
                if (!this.accepted) return 0;
                let totalProgress = 0;
                let totalTarget = 0;
                for (const objective of this.objectives) {
                    totalProgress += this.progress[objective.id] || 0;
                    totalTarget += objective.target;
                }
                return totalTarget > 0 ? Math.min(100, (totalProgress / totalTarget) * 100) : 0;
            }
        }

        // ===== КЛАСС СОБЫТИЯ =====
        class GameEvent {
            constructor(id, name, description, duration, trigger, effect, icon = "fas fa-bolt") {
                this.id = id;
                this.name = name;
                this.description = description;
                this.duration = duration;
                this.trigger = trigger;
                this.effect = effect;
                this.icon = icon;
                this.active = false;
                this.startTime = null;
                this.endTime = null;
            }

            check(game) {
                if (!this.active && this.trigger(game)) {
                    this.activate(game);
                    return true;
                }
                return false;
            }

            activate(game) {
                this.active = true;
                this.startTime = Date.now();
                this.endTime = this.startTime + this.duration;
                
                // Применяем эффект
                if (this.effect.onStart) {
                    this.effect.onStart(game);
                }
                
                return true;
            }

            update(game) {
                if (this.active && Date.now() >= this.endTime) {
                    this.deactivate(game);
                    return true;
                }
                return false;
            }

            deactivate(game) {
                this.active = false;
                
                // Отменяем эффект
                if (this.effect.onEnd) {
                    this.effect.onEnd(game);
                }
                
                return true;
            }

            getRemainingTime() {
                if (!this.active) return 0;
                return Math.max(0, this.endTime - Date.now());
            }

            getProgressPercent() {
                if (!this.active || !this.startTime || !this.endTime) return 0;
                const elapsed = Date.now() - this.startTime;
                const total = this.endTime - this.startTime;
                return Math.min(100, (elapsed / total) * 100);
            }
        }

        // ===== ОСНОВНОЙ КЛАСС ИГРЫ =====
        class SpaceClickerGame {
            constructor() {
                this.version = CONFIG.VERSION;
                this.startTime = Date.now();
                this.playTime = 0;
                this.lastUpdate = Date.now();
                this.isInitialized = false;
                
                // Основные ресурсы
                this.resources = {};
                this.initializeResources();
                
                // Игровые системы
                this.upgrades = [];
                this.automations = [];
                this.achievements = [];
                this.researches = [];
                this.quests = [];
                this.events = [];
                this.craftingRecipes = [];
                this.prestigeUpgrades = [];
                this.skillTree = [];
                
                // Статистика
                this.stats = {
                    totalClicks: 0,
                    totalEnergy: 0,
                    totalPrestiges: 0,
                    maxEnergy: 0,
                    maxLevel: 1,
                    clicksPerSecond: 0,
                    highestMultiplier: 1,
                    upgradesBought: 0,
                    automationsBought: 0,
                    researchesCompleted: 0,
                    questsCompleted: 0,
                    achievementsUnlocked: 0,
                    playTime: 0
                };
                
                // Игровые настройки
                this.settings = {
                    autoSave: true,
                    notifications: true,
                    sound: true,
                    particles: true,
                    animations: true,
                    theme: 'dark'
                };
                
                // Множители
                this.multipliers = {
                    energy: 1,
                    click: 1,
                    production: 1,
                    research: 1,
                    prestige: 1
                };
                
                // Состояние игры
                this.level = 1;
                this.experience = 0;
                this.experienceToNextLevel = 100;
                this.prestigePoints = 0;
                this.prestigeLevel = 0;
                this.clickMultiplier = 1;
                this.lastClickTime = 0;
                this.clickCombo = 0;
                this.maxClickCombo = 0;
                this.comboTimeout = null;
                
                // Оффлайн прогресс
                this.lastSaveTime = Date.now();
                
                // Системные переменные
                this.notificationQueue = [];
                this.activeModals = [];
                this.intervalIds = [];
                
                this.initializeGameSystems();
            }

            // ===== ИНИЦИАЛИЗАЦИЯ =====
            initializeResources() {
                // Основные ресурсы
                this.resources.energy = new Resource('energy', 'Энергия', 'fas fa-bolt', '#f1c40f', 'Основная энергия квантового синтеза', 0, Infinity);
                this.resources.metal = new Resource('metal', 'Металл', 'fas fa-cog', '#bdc3c7', 'Базовый строительный материал', 0, 1e9);
                this.resources.crystals = new Resource('crystals', 'Кристаллы', 'fas fa-gem', '#3498db', 'Фокусирующие кристаллы', 0, 1e6);
                this.resources.uranium = new Resource('uranium', 'Уран', 'fas fa-radiation', '#2ecc71', 'Радиоактивное топливо', 0, 1e6);
                this.resources.antimatter = new Resource('antimatter', 'Антиматерия', 'fas fa-atom', '#e74c3c', 'Экзотическая материя', 0, 1e4);
                this.resources.darkMatter = new Resource('darkMatter', 'Темная материя', 'fas fa-moon', '#2c3e50', 'Загадочная субстанция', 0, 1e3);
                this.resources.quantum = new Resource('quantum', 'Квантовые частицы', 'fas fa-atom', '#9b59b6', 'Фундаментальные частицы', 0, 1e5);
                
                // Продвинутые ресурсы
                this.resources.science = new Resource('science', 'Наука', 'fas fa-flask', '#0984e3', 'Исследовательские очки', 0, 1e6);
                this.resources.technology = new Resource('technology', 'Технологии', 'fas fa-microchip', '#00cec9', 'Технологические очки', 0, 1e4);
                this.resources.galactic = new Resource('galactic', 'Галактические кредиты', 'fas fa-coins', '#f39c12', 'Межгалактическая валюта', 0, Infinity);
                this.resources.prestige = new Resource('prestige', 'Очки престижа', 'fas fa-star', '#fd79a8', 'Очки для улучшений престижа', 0, Infinity);
                
                // Экзотические ресурсы
                this.resources.nebula = new Resource('nebula', 'Туманность', 'fas fa-cloud', '#8e44ad', 'Энергия туманностей', 0, 1e3);
                this.resources.singularity = new Resource('singularity', 'Сингулярность', 'fas fa-dharmachakra', '#e67e22', 'Энергия черных дыр', 0, 1e2);
                this.resources.multiverse = new Resource('multiverse', 'Мультивселенная', 'fas fa-infinity', '#6c5ce7', 'Энергия параллельных вселенных', 0, 50);
            }

            initializeGameSystems() {
                // Инициализация улучшений
                this.initializeUpgrades();
                
                // Инициализация автоматизации
                this.initializeAutomations();
                
                // Инициализация достижений
                this.initializeAchievements();
                
                // Инициализация исследований
                this.initializeResearches();
                
                // Инициализация квестов
                this.initializeQuests();
                
                // Инициализация событий
                this.initializeEvents();
                
                // Инициализация крафтинга
                this.initializeCrafting();
                
                // Инициализация престиж улучшений
                this.initializePrestigeUpgrades();
                
                // Инициализация дерева навыков
                this.initializeSkillTree();
                
                this.isInitialized = true;
            }

            initializeUpgrades() {
                // Улучшения кликов
                this.upgrades.push(new Upgrade(
                    'click_1',
                    'Улучшенный клик',
                    'Увеличивает энергию за клик',
                    50,
                    'click',
                    { type: 'clickPower', value: 2 },
                    50,
                    1.15
                ));

                this.upgrades.push(new Upgrade(
                    'click_2',
                    'Мощный клик',
                    'Значительно увеличивает энергию за клик',
                    250,
                    'click',
                    { type: 'clickPower', value: 5 },
                    25,
                    1.25
                ));

                this.upgrades.push(new Upgrade(
                    'click_3',
                    'Квантовый клик',
                    'Использует квантовую неопределенность',
                    1000,
                    'click',
                    { type: 'clickPower', value: () => 10 + this.level * 0.5 },
                    10,
                    1.5
                ));

                // Улучшения производства
                this.upgrades.push(new Upgrade(
                    'prod_1',
                    'Улучшенные генераторы',
                    'Увеличивает производство энергии',
                    100,
                    'production',
                    { type: 'energyPerSecond', value: 1 },
                    100,
                    1.12
                ));

                this.upgrades.push(new Upgrade(
                    'prod_2',
                    'Квантовые генераторы',
                    'Использует квантовое туннелирование',
                    5000,
                    'production',
                    { type: 'energyPerSecond', value: () => 5 * Math.pow(1.1, this.level) },
                    50,
                    1.3
                ));

                // Мультипликаторы
                this.upgrades.push(new Upgrade(
                    'mult_1',
                    'Мультипликатор энергии',
                    'Увеличивает все получаемые ресурсы',
                    1000,
                    'multiplier',
                    { type: 'globalMultiplier', value: 0.1 },
                    20,
                    2.0
                ));

                // Особые улучшения
                this.upgrades.push(new Upgrade(
                    'special_1',
                    'Автокликер',
                    'Автоматически кликает каждую секунду',
                    50000,
                    'special',
                    { type: 'autoClick', value: 1 },
                    1,
                    1
                ));

                this.upgrades.push(new Upgrade(
                    'special_2',
                    'Квантовый разлом',
                    'Шанс получить бонусные ресурсы при клике',
                    100000,
                    'special',
                    { type: 'quantumBonus', value: 0.05 },
                    10,
                    1.8
                ));
            }

            initializeAutomations() {
                this.automations.push(new Automation(
                    'auto_energy_1',
                    'Солнечная панель',
                    'Производит энергию из солнечного света',
                    100,
                    0.1,
                    'energy'
                ));

                this.automations.push(new Automation(
                    'auto_metal_1',
                    'Автоматический шахтер',
                    'Добывает металл автоматически',
                    500,
                    0.5,
                    'metal'
                ));

                this.automations.push(new Automation(
                    'auto_crystal_1',
                    'Кристальный экстрактор',
                    'Добывает кристаллы автоматически',
                    1000,
                    0.1,
                    'crystals'
                ));

                this.automations.push(new Automation(
                    'auto_quantum_1',
                    'Квантовый реактор',
                    'Производит квантовые частицы',
                    10000,
                    0.01,
                    'quantum'
                ));
            }

            initializeAchievements() {
                // Базовые достижения
                this.achievements.push(new Achievement(
                    'ach_energy_100',
                    'Первая энергия',
                    'Соберите 100 энергии',
                    (game) => game.resources.energy.total >= 100,
                    (game) => {
                        game.resources.energy.add(1000);
                        game.showNotification('Получено достижение: Первая энергия! +1000 энергии', 'success');
                    },
                    'fas fa-bolt',
                    1
                ));

                this.achievements.push(new Achievement(
                    'ach_energy_1000',
                    'Энергетик',
                    'Соберите 1,000 энергии',
                    (game) => game.resources.energy.total >= 1000,
                    (game) => {
                        game.multipliers.energy *= 1.5;
                        game.showNotification('Получено достижение: Энергетик! Мультипликатор энергии ×1.5', 'success');
                    },
                    'fas fa-bolt',
                    2
                ));

                this.achievements.push(new Achievement(
                    'ach_clicks_100',
                    'Мастер кликов',
                    'Сделайте 100 кликов',
                    (game) => ({ progress: game.stats.totalClicks, max: 100 }),
                    (game) => {
                        game.clickMultiplier *= 1.2;
                        game.showNotification('Получено достижение: Мастер кликов! Мультипликатор кликов ×1.2', 'success');
                    },
                    'fas fa-mouse',
                    1
                ));

                // Продвинутые достижения
                this.achievements.push(new Achievement(
                    'ach_level_10',
                    'Опытный исследователь',
                    'Достигните 10 уровня',
                    (game) => game.level >= 10,
                    (game) => {
                        game.multipliers.research *= 2;
                        game.showNotification('Получено достижение: Опытный исследователь! Мультипликатор исследований ×2', 'success');
                    },
                    'fas fa-user-astronaut',
                    3
                ));

                // Престижные достижения
                this.achievements.push(new Achievement(
                    'ach_prestige_1',
                    'Первое перерождение',
                    'Выполните первое престижное перерождение',
                    (game) => game.prestigeLevel >= 1,
                    (game) => {
                        game.prestigePoints += 10;
                        game.showNotification('Получено достижение: Первое перерождение! +10 очков престижа', 'prestige');
                    },
                    'fas fa-redo',
                    4
                ));
            }

            initializeResearches() {
                this.researches.push(new Research(
                    'res_quantum_1',
                    'Квантовая механика',
                    'Изучение основ квантовой физики',
                    1000,
                    60,
                    [(game) => game.level >= 5],
                    (game) => {
                        game.resources.quantum.perSecond += 0.1;
                        game.showNotification('Исследование завершено: Квантовая механика! +0.1 квантовых частиц в секунду', 'info');
                    },
                    'fas fa-atom',
                    1
                ));

                this.researches.push(new Research(
                    'res_singularity_1',
                    'Теория сингулярности',
                    'Изучение черных дыр и сингулярностей',
                    5000,
                    300,
                    [(game) => game.level >= 15, (game) => game.researches[0].completed],
                    (game) => {
                        game.resources.singularity.max += 10;
                        game.showNotification('Исследование завершено: Теория сингулярности! +10 максимальной сингулярности', 'info');
                    },
                    'fas fa-dharmachakra',
                    2
                ));
            }

            initializeQuests() {
                this.quests.push(new Quest(
                    'quest_energy_rush',
                    'Энергетический рывок',
                    'Соберите большое количество энергии за ограниченное время',
                    [
                        { id: 'energy', target: 10000, check: (game) => game.resources.energy.total }
                    ],
                    [
                        (game) => game.resources.galactic.add(1000),
                        (game) => game.resources.science.add(500)
                    ],
                    60000, // 1 минута
                    true
                ));
            }

            initializeEvents() {
                this.events.push(new GameEvent(
                    'event_solar_flare',
                    'Солнечная вспышка',
                    'Мощная солнечная вспышка увеличивает производство энергии',
                    30000,
                    (game) => Math.random() < 0.001 && game.resources.energy.total > 1000,
                    {
                        onStart: (game) => {
                            game.multipliers.energy *= 3;
                            game.showNotification('Солнечная вспышка! Производство энергии увеличено в 3 раза на 30 секунд', 'warning');
                        },
                        onEnd: (game) => {
                            game.multipliers.energy /= 3;
                            game.showNotification('Солнечная вспышка закончилась', 'info');
                        }
                    },
                    'fas fa-sun'
                ));
            }

            initializeCrafting() {
                this.craftingRecipes.push({
                    id: 'craft_energy_core',
                    name: 'Энергетическое ядро',
                    description: 'Мощный источник энергии',
                    cost: {
                        metal: 100,
                        crystals: 50,
                        energy: 1000
                    },
                    result: (game) => {
                        game.resources.energy.add(10000);
                        game.showNotification('Создано энергетическое ядро! +10,000 энергии', 'success');
                    },
                    unlocked: true
                });
            }

            initializePrestigeUpgrades() {
                this.prestigeUpgrades.push({
                    id: 'prestige_mult_1',
                    name: 'Вечный мультипликатор',
                    description: 'Увеличивает базовый мультипликатор на 10%',
                    cost: 1,
                    effect: (game) => {
                        game.multipliers.prestige *= 1.1;
                    },
                    purchased: false
                });
            }

            initializeSkillTree() {
                this.skillTree.push({
                    id: 'skill_click_power',
                    name: 'Сила клика',
                    description: 'Увеличивает энергию за клик на 25%',
                    cost: 1,
                    requirements: [],
                    effect: (game) => {
                        game.clickMultiplier *= 1.25;
                    },
                    purchased: false
                });
            }

            // ===== ОСНОВНЫЕ МЕТОДЫ ИГРЫ =====
            click() {
                const now = Date.now();
                
                // Проверка кулдауна
                if (now - this.lastClickTime < CONFIG.CLICK_COOLDOWN) {
                    return;
                }
                
                // Расчет комбо
                if (now - this.lastClickTime < 1000) {
                    this.clickCombo++;
                    this.maxClickCombo = Math.max(this.maxClickCombo, this.clickCombo);
                } else {
                    this.clickCombo = 1;
                }
                
                // Сброс таймера комбо
                if (this.comboTimeout) {
                    clearTimeout(this.comboTimeout);
                }
                this.comboTimeout = setTimeout(() => {
                    this.clickCombo = 0;
                }, 1000);
                
                // Базовый клик
                let clickEnergy = 1;
                
                // Модификаторы улучшений
                for (const upgrade of this.upgrades) {
                    if (upgrade.purchased && upgrade.effect.type === 'clickPower') {
                        clickEnergy += upgrade.getEffectValue();
                    }
                }
                
                // Множители
                clickEnergy *= this.clickMultiplier;
                clickEnergy *= this.multipliers.click;
                clickEnergy *= this.multipliers.energy;
                
                // Бонус комбо
                if (this.clickCombo > 1) {
                    const comboBonus = 1 + (this.clickCombo * 0.05);
                    clickEnergy *= comboBonus;
                }
                
                // Квантовый бонус
                for (const upgrade of this.upgrades) {
                    if (upgrade.purchased && upgrade.effect.type === 'quantumBonus') {
                        if (Math.random() < upgrade.getEffectValue()) {
                            clickEnergy *= 2;
                            this.showNotification('Квантовый бонус! Клик удвоен', 'info');
                        }
                    }
                }
                
                // Добавление энергии
                const actualEnergy = clickEnergy * this.multipliers.prestige;
                this.resources.energy.add(actualEnergy);
                
                // Обновление статистики
                this.stats.totalClicks++;
                this.stats.totalEnergy += actualEnergy;
                this.stats.maxEnergy = Math.max(this.stats.maxEnergy, this.resources.energy.value);
                this.stats.clicksPerSecond = this.stats.totalClicks / (this.playTime / 1000);
                
                // Опыт
                this.addExperience(clickEnergy * 0.1);
                
                // Обновление времени последнего клика
                this.lastClickTime = now;
                
                // Проверка достижений
                this.checkAchievements();
                
                // Создание частиц
                if (this.settings.particles) {
                    this.createClickParticles(actualEnergy);
                }
                
                return {
                    energy: actualEnergy,
                    combo: this.clickCombo,
                    isCritical: false
                };
            }

            addExperience(amount) {
                this.experience += amount * this.multipliers.research;
                
                while (this.experience >= this.experienceToNextLevel) {
                    this.experience -= this.experienceToNextLevel;
                    this.levelUp();
                }
            }

            levelUp() {
                this.level++;
                this.stats.maxLevel = Math.max(this.stats.maxLevel, this.level);
                this.experienceToNextLevel = Math.floor(100 * Math.pow(1.2, this.level));
                
                // Награда за уровень
                const levelReward = 100 * this.level * this.multipliers.prestige;
                this.resources.energy.add(levelReward);
                
                // Улучшение клика с уровнем
                this.clickMultiplier *= 1.05;
                
                this.showNotification(`Уровень ${this.level} достигнут! +${formatNumber(levelReward)} энергии`, 'success');
                
                // Проверка достижений
                this.checkAchievements();
            }

            update(deltaTime) {
                const now = Date.now();
                this.playTime += deltaTime;
                
                // Производство ресурсов
                for (const resource of Object.values(this.resources)) {
                    resource.produce(deltaTime);
                }
                
                // Обновление автоматизации
                for (const automation of this.automations) {
                    if (automation.count > 0) {
                        const production = automation.getTotalProduction() * deltaTime / 1000;
                        this.resources[automation.resourceId].add(production);
                    }
                }
                
                // Обновление исследований
                for (const research of this.researches) {
                    if (research.inProgress) {
                        if (research.update(deltaTime)) {
                            this.showNotification(`Исследование "${research.name}" завершено!`, 'info');
                        }
                    }
                }
                
                // Обновление квестов
                for (const quest of this.quests) {
                    if (quest.accepted && !quest.completed) {
                        quest.update(this);
                    }
                }
                
                // Проверка событий
                for (const event of this.events) {
                    event.check(this);
                    if (event.active) {
                        event.update(this);
                    }
                }
                
                // Автокликер
                const autoClicker = this.upgrades.find(u => u.id === 'special_1');
                if (autoClicker && autoClicker.purchased) {
                    const autoClicks = autoClicker.getEffectValue() * deltaTime / 1000;
                    for (let i = 0; i < Math.floor(autoClicks); i++) {
                        this.click();
                    }
                }
                
                this.lastUpdate = now;
            }

            prestige() {
                if (this.resources.energy.total < 1e6) {
                    this.showNotification('Требуется хотя бы 1,000,000 энергии для престижа', 'error');
                    return false;
                }
                
                // Расчет очков престижа
                const prestigePoints = Math.floor(Math.sqrt(this.resources.energy.total / 1e6) * 10);
                
                // Сохранение некоторых данных
                const oldPrestigeLevel = this.prestigeLevel;
                const oldPrestigePoints = this.prestigePoints;
                
                // Сброс игры
                this.resetForPrestige();
                
                // Добавление очков престижа
                this.prestigePoints += prestigePoints;
                this.prestigeLevel++;
                this.stats.totalPrestiges++;
                
                // Сохранение достижений
                for (const achievement of this.achievements) {
                    if (achievement.tier >= 4) {
                        achievement.unlocked = false;
                    }
                }
                
                this.showNotification(
                    `Престиж выполнен! Уровень престижа: ${this.prestigeLevel}. Получено очков: ${prestigePoints}`,
                    'prestige'
                );
                
                // Проверка достижений престижа
                this.checkAchievements();
                
                return true;
            }

            resetForPrestige() {
                // Сброс ресурсов
                for (const resource of Object.values(this.resources)) {
                    resource.value = 0;
                    resource.total = 0;
                }
                
                // Сброс улучшений
                for (const upgrade of this.upgrades) {
                    upgrade.level = 0;
                    upgrade.purchased = false;
                    upgrade.cost = upgrade.baseCost;
                }
                
                // Сброс автоматизации
                for (const automation of this.automations) {
                    automation.count = 0;
                    automation.cost = automation.baseCost || 100;
                }
                
                // Сброс исследований
                for (const research of this.researches) {
                    research.completed = false;
                    research.inProgress = false;
                    research.progress = 0;
                }
                
                // Сброс уровня
                this.level = 1;
                this.experience = 0;
                this.experienceToNextLevel = 100;
                
                // Сброс комбо
                this.clickCombo = 0;
                this.maxClickCombo = 0;
                
                // Сохранение некоторых множителей
                const oldClickMultiplier = this.clickMultiplier;
                this.clickMultiplier = 1;
                
                // Применение престижных бонусов
                for (const upgrade of this.prestigeUpgrades) {
                    if (upgrade.purchased && upgrade.effect) {
                        upgrade.effect(this);
                    }
                }
                
                // Применение навыков
                for (const skill of this.skillTree) {
                    if (skill.purchased && skill.effect) {
                        skill.effect(this);
                    }
                }
            }

            checkAchievements() {
                let newAchievements = 0;
                for (const achievement of this.achievements) {
                    if (!achievement.unlocked && achievement.check(this)) {
                        newAchievements++;
                    }
                }
                return newAchievements;
            }

            // ===== ВСПОМОГАТЕЛЬНЫЕ МЕТОДЫ =====
            showNotification(message, type = 'info') {
                if (!this.settings.notifications) return;
                
                const notification = {
                    id: Date.now() + Math.random(),
                    type,
                    message,
                    timestamp: Date.now()
                };
                
                this.notificationQueue.push(notification);
                
                // Ограничение очереди
                if (this.notificationQueue.length > 10) {
                    this.notificationQueue.shift();
                }
                
                return notification.id;
            }

            createClickParticles(energy) {
                if (!this.settings.particles) return;
                
                const clickButton = document.getElementById('clickButton');
                if (!clickButton) return;
                
                const particleCount = Math.min(20, Math.floor(energy / 10));
                
                for (let i = 0; i < particleCount; i++) {
                    const particle = document.createElement('div');
                    particle.className = 'click-particle';
                    particle.style.position = 'absolute';
                    particle.style.width = `${Math.random() * 10 + 5}px`;
                    particle.style.height = particle.style.width;
                    particle.style.background = `radial-gradient(circle, ${getRandomColor()}, transparent)`;
                    particle.style.borderRadius = '50%';
                    particle.style.left = '50%';
                    particle.style.top = '50%';
                    particle.style.transform = 'translate(-50%, -50%)';
                    particle.style.zIndex = '5';
                    particle.style.pointerEvents = 'none';
                    
                    // Случайное направление
                    const angle = Math.random() * Math.PI * 2;
                    const distance = Math.random() * 100 + 50;
                    const tx = Math.cos(angle) * distance;
                    const ty = Math.sin(angle) * distance;
                    
                    particle.style.setProperty('--tx', `${tx}px`);
                    particle.style.setProperty('--ty', `${ty}px`);
                    particle.style.animation = `particle-trail ${Math.random() * 0.5 + 0.3}s ease-out forwards`;
                    
                    clickButton.appendChild(particle);
                    
                    // Удаление частицы после анимации
                    setTimeout(() => {
                        if (particle.parentNode === clickButton) {
                            clickButton.removeChild(particle);
                        }
                    }, 800);
                }
            }

            getSaveData() {
                return {
                    version: this.version,
                    resources: Object.fromEntries(Object.entries(this.resources).map(([id, res]) => [
                        id,
                        {
                            value: res.value,
                            total: res.total,
                            unlocked: res.unlocked
                        }
                    ])),
                    upgrades: this.upgrades.map(upgrade => ({
                        id: upgrade.id,
                        level: upgrade.level,
                        purchased: upgrade.purchased
                    })),
                    automations: this.automations.map(auto => ({
                        id: auto.id,
                        count: auto.count,
                        cost: auto.cost
                    })),
                    achievements: this.achievements.map(ach => ({
                        id: ach.id,
                        unlocked: ach.unlocked,
                        progress: ach.progress
                    })),
                    researches: this.researches.map(res => ({
                        id: res.id,
                        completed: res.completed,
                        inProgress: res.inProgress,
                        progress: res.progress
                    })),
                    stats: this.stats,
                    level: this.level,
                    experience: this.experience,
                    experienceToNextLevel: this.experienceToNextLevel,
                    prestigePoints: this.prestigePoints,
                    prestigeLevel: this.prestigeLevel,
                    clickMultiplier: this.clickMultiplier,
                    multipliers: this.multipliers,
                    settings: this.settings,
                    playTime: this.playTime + (Date.now() - this.lastUpdate),
                    lastSaveTime: Date.now()
                };
            }

            loadSaveData(data) {
                try {
                    // Проверка версии
                    if (data.version !== this.version) {
                        this.showNotification(`Версия сохранения (${data.version}) отличается от текущей (${this.version})`, 'warning');
                    }
                    
                    // Загрузка ресурсов
                    if (data.resources) {
                        for (const [id, save] of Object.entries(data.resources)) {
                            if (this.resources[id]) {
                                this.resources[id].value = save.value || 0;
                                this.resources[id].total = save.total || 0;
                                this.resources[id].unlocked = save.unlocked || false;
                            }
                        }
                    }
                    
                    // Загрузка улучшений
                    if (data.upgrades) {
                        for (const save of data.upgrades) {
                            const upgrade = this.upgrades.find(u => u.id === save.id);
                            if (upgrade) {
                                upgrade.level = save.level || 0;
                                upgrade.purchased = save.purchased || false;
                                if (upgrade.level > 0) {
                                    upgrade.cost = upgrade.getNextCost();
                                }
                            }
                        }
                    }
                    
                    // Загрузка автоматизации
                    if (data.automations) {
                        for (const save of data.automations) {
                            const auto = this.automations.find(a => a.id === save.id);
                            if (auto) {
                                auto.count = save.count || 0;
                                auto.cost = save.cost || auto.baseCost;
                            }
                        }
                    }
                    
                    // Загрузка достижений
                    if (data.achievements) {
                        for (const save of data.achievements) {
                            const ach = this.achievements.find(a => a.id === save.id);
                            if (ach) {
                                ach.unlocked = save.unlocked || false;
                                ach.progress = save.progress || 0;
                            }
                        }
                    }
                    
                    // Загрузка исследований
                    if (data.researches) {
                        for (const save of data.researches) {
                            const res = this.researches.find(r => r.id === save.id);
                            if (res) {
                                res.completed = save.completed || false;
                                res.inProgress = save.inProgress || false;
                                res.progress = save.progress || 0;
                            }
                        }
                    }
                    
                    // Загрузка статистики
                    if (data.stats) {
                        Object.assign(this.stats, data.stats);
                    }
                    
                    // Загрузка состояния игры
                    this.level = data.level || 1;
                    this.experience = data.experience || 0;
                    this.experienceToNextLevel = data.experienceToNextLevel || 100;
                    this.prestigePoints = data.prestigePoints || 0;
                    this.prestigeLevel = data.prestigeLevel || 0;
                    this.clickMultiplier = data.clickMultiplier || 1;
                    
                    // Загрузка множителей
                    if (data.multipliers) {
                        Object.assign(this.multipliers, data.multipliers);
                    }
                    
                    // Загрузка настроек
                    if (data.settings) {
                        Object.assign(this.settings, data.settings);
                    }
                    
                    // Расчет оффлайн прогресса
                    if (data.lastSaveTime) {
                        const offlineTime = Date.now() - data.lastSaveTime;
                        const offlineSeconds = Math.min(offlineTime / 1000, CONFIG.OFFLINE_MAX_TIME);
                        
                        if (offlineSeconds > 0) {
                            this.update(offlineSeconds * 1000);
                            this.showNotification(
                                `Оффлайн прогресс: ${formatNumber(offlineSeconds)} секунд`,
                                'info'
                            );
                        }
                    }
                    
                    this.playTime = data.playTime || 0;
                    this.lastUpdate = Date.now();
                    
                    this.showNotification('Игра успешно загружена!', 'success');
                    return true;
                    
                } catch (error) {
                    console.error('Ошибка загрузки сохранения:', error);
                    this.showNotification('Ошибка загрузки сохранения', 'error');
                    return false;
                }
            }

            exportSave() {
                const saveData = this.getSaveData();
                const json = JSON.stringify(saveData, null, 2);
                const blob = new Blob([json], { type: 'application/json' });
                const url = URL.createObjectURL(blob);
                
                const a = document.createElement('a');
                a.href = url;
                a.download = `space_clicker_save_${Date.now()}.json`;
                document.body.appendChild(a);
                a.click();
                document.body.removeChild(a);
                URL.revokeObjectURL(url);
                
                this.showNotification('Сохранение экспортировано', 'success');
            }

            importSave(json) {
                try {
                    const data = JSON.parse(json);
                    if (this.loadSaveData(data)) {
                        this.showNotification('Сохранение импортировано', 'success');
                        return true;
                    }
                } catch (error) {
                    console.error('Ошибка импорта:', error);
                    this.showNotification('Ошибка импорта сохранения', 'error');
                }
                return false;
            }

            // ===== GETTERS =====
            getEnergyPerSecond() {
                let eps = 0;
                
                // От автоматизации
                for (const automation of this.automations) {
                    if (automation.resourceId === 'energy') {
                        eps += automation.getTotalProduction();
                    }
                }
                
                // От улучшений
                for (const upgrade of this.upgrades) {
                    if (upgrade.purchased && upgrade.effect.type === 'energyPerSecond') {
                        eps += upgrade.getEffectValue();
                    }
                }
                
                return eps * this.multipliers.energy * this.multipliers.production * this.multipliers.prestige;
            }

            getClickPower() {
                let power = 1;
                
                for (const upgrade of this.upgrades) {
                    if (upgrade.purchased && upgrade.effect.type === 'clickPower') {
                        power += upgrade.getEffectValue();
                    }
                }
                
                return power * this.clickMultiplier * this.multipliers.click * this.multipliers.energy * this.multipliers.prestige;
            }

            getGlobalMultiplier() {
                return this.multipliers.energy * this.multipliers.prestige;
            }

            getLevelProgressPercent() {
                return (this.experience / this.experienceToNextLevel) * 100;
            }

            // ===== СИСТЕМНЫЕ МЕТОДЫ =====
            startGameLoop() {
                // Основной игровой цикл
                this.intervalIds.push(setInterval(() => {
                    const now = Date.now();
                    const deltaTime = now - this.lastUpdate;
                    
                    this.update(deltaTime);
                    this.lastUpdate = now;
                    
                    // Автосохранение
                    if (this.settings.autoSave && now - this.lastSaveTime > CONFIG.AUTOSAVE_INTERVAL) {
                        this.saveGame();
                    }
                    
                }, CONFIG.TICK_INTERVAL));
                
                // Обработка уведомлений
                this.intervalIds.push(setInterval(() => {
                    this.processNotificationQueue();
                }, 100));
            }

            stopGameLoop() {
                for (const id of this.intervalIds) {
                    clearInterval(id);
                }
                this.intervalIds = [];
            }

            processNotificationQueue() {
                if (this.notificationQueue.length === 0) return;
                
                const notification = this.notificationQueue.shift();
                this.displayNotification(notification);
            }

            displayNotification(notification) {
                const container = document.getElementById('notificationContainer');
                if (!container) return;
                
                const notificationEl = document.createElement('div');
                notificationEl.className = `notification ${notification.type}`;
                notificationEl.innerHTML = `
                    <div class="notification-header">
                        <div class="notification-title">
                            <i class="fas fa-${getNotificationIcon(notification.type)}"></i>
                            ${getNotificationTitle(notification.type)}
                        </div>
                        <button class="notification-close">
                            <i class="fas fa-times"></i>
                        </button>
                    </div>
                    <div class="notification-content">${notification.message}</div>
                `;
                
                container.appendChild(notificationEl);
                
                // Показ с анимацией
                setTimeout(() => {
                    notificationEl.classList.add('show');
                }, 10);
                
                // Закрытие по кнопке
                const closeBtn = notificationEl.querySelector('.notification-close');
                closeBtn.addEventListener('click', () => {
                    notificationEl.classList.remove('show');
                    setTimeout(() => {
                        if (notificationEl.parentNode === container) {
                            container.removeChild(notificationEl);
                        }
                    }, 500);
                });
                
                // Автоматическое закрытие
                setTimeout(() => {
                    if (notificationEl.parentNode === container) {
                        notificationEl.classList.remove('show');
                        setTimeout(() => {
                            if (notificationEl.parentNode === container) {
                                container.removeChild(notificationEl);
                            }
                        }, 500);
                    }
                }, CONFIG.NOTIFICATION_DURATION);
            }

            saveGame() {
                try {
                    const saveData = this.getSaveData();
                    localStorage.setItem(CONFIG.SAVE_KEY, JSON.stringify(saveData));
                    this.lastSaveTime = Date.now();
                    
                    if (this.settings.notifications) {
                        this.showNotification('Игра сохранена', 'success');
                    }
                    
                    return true;
                } catch (error) {
                    console.error('Ошибка сохранения:', error);
                    this.showNotification('Ошибка сохранения', 'error');
                    return false;
                }
            }

            loadGame() {
                try {
                    const saveData = localStorage.getItem(CONFIG.SAVE_KEY);
                    if (!saveData) {
                        this.showNotification('Создана новая игра', 'info');
                        return false;
                    }
                    
                    const data = JSON.parse(saveData);
                    return this.loadSaveData(data);
                } catch (error) {
                    console.error('Ошибка загрузки:', error);
                    this.showNotification('Ошибка загрузки сохранения', 'error');
                    return false;
                }
            }

            resetGame() {
                if (confirm('Вы уверены, что хотите сбросить весь прогресс? Это действие нельзя отменить.')) {
                    localStorage.removeItem(CONFIG.SAVE_KEY);
                    
                    // Создание новой игры
                    Object.assign(this, new SpaceClickerGame());
                    this.initializeGameSystems();
                    
                    this.showNotification('Игра сброшена', 'info');
                    return true;
                }
                return false;
            }
        }

        // ===== ВСПОМОГАТЕЛЬНЫЕ ФУНКЦИИ =====
        function formatNumber(num) {
            if (num === 0) return '0';
            if (num < 0.0001) return num.toExponential(2);
            if (num < 1) return num.toFixed(4);
            if (num < 1000) return Math.floor(num).toString();
            
            const suffixes = ['', 'K', 'M', 'B', 'T', 'Qa', 'Qi', 'Sx', 'Sp', 'Oc', 'No'];
            const tier = Math.floor(Math.log10(num) / 3);
            
            if (tier === 0) return Math.floor(num).toString();
            
            const suffix = suffixes[tier];
            const scale = Math.pow(10, tier * 3);
            const scaled = num / scale;
            
            if (scaled < 10) return scaled.toFixed(2) + suffix;
            if (scaled < 100) return scaled.toFixed(1) + suffix;
            return Math.floor(scaled) + suffix;
        }

        function getRandomColor() {
            const colors = [
                '#00cec9', '#fd79a8', '#6c5ce7', '#a29bfe',
                '#fdcb6e', '#00b894', '#0984e3', '#d63031'
            ];
            return colors[Math.floor(Math.random() * colors.length)];
        }

        function getNotificationIcon(type) {
            switch(type) {
                case 'success': return 'check-circle';
                case 'warning': return 'exclamation-triangle';
                case 'error': return 'times-circle';
                case 'prestige': return 'star';
                default: return 'info-circle';
            }
        }

        function getNotificationTitle(type) {
            switch(type) {
                case 'success': return 'Успех';
                case 'warning': return 'Внимание';
                case 'error': return 'Ошибка';
                case 'prestige': return 'Престиж';
                default: return 'Информация';
            }
        }

        function createStars() {
            const starsContainer = document.getElementById('stars');
            if (!starsContainer) return;
            
            // Очистка старых звезд
            starsContainer.innerHTML = '';
            
            const starCount = 500;
            
            for (let i = 0; i < starCount; i++) {
                const star = document.createElement('div');
                star.className = 'star';
                
                // Размер
                const size = Math.random() * 4;
                star.style.width = `${size}px`;
                star.style.height = `${size}px`;
                
                // Позиция
                const x = Math.random() * 100;
                const y = Math.random() * 100;
                star.style.left = `${x}%`;
                star.style.top = `${y}%`;
                
                // Яркость
                const brightness = 0.2 + Math.random() * 0.8;
                star.style.opacity = brightness;
                
                // Цвет
                if (Math.random() > 0.9) {
                    const colors = ['#00cec9', '#fd79a8', '#fdcb6e'];
                    star.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                }
                
                // Анимация
                const duration = 2 + Math.random() * 4;
                const delay = Math.random() * 5;
                star.style.setProperty('--twinkle-duration', `${duration}s`);
                star.style.setProperty('--twinkle-delay', `${delay}s`);
                
                starsContainer.appendChild(star);
            }
        }

        // ===== ИНИЦИАЛИЗАЦИЯ UI =====
        class GameUI {
            constructor(game) {
                this.game = game;
                this.lastUpdate = Date.now();
                this.updateInterval = null;
                this.isInitialized = false;
            }

            initialize() {
                console.log('Инициализация UI...');
                
                // Создание звездного фона
                createStars();
                
                // Настройка обработчиков событий
                this.setupEventListeners();
                
                // Инициализация всех UI компонентов
                this.initializeResourcesUI();
                this.initializeUpgradesUI();
                this.initializeAutomationUI();
                this.initializeAchievementsUI();
                this.initializeResearchUI();
                this.initializePrestigeUI();
                this.initializeCraftingUI();
                this.initializeSettingsUI();
                
                // Обновление UI
                this.updateAllUI();
                
                // Запуск обновления UI
                this.startUILoop();
                
                // Скрытие экрана загрузки
                setTimeout(() => {
                    const loadingScreen = document.getElementById('loadingScreen');
                    if (loadingScreen) {
                        loadingScreen.style.opacity = '0';
                        setTimeout(() => {
                            loadingScreen.style.display = 'none';
                        }, 500);
                    }
                }, 1500);
                
                this.isInitialized = true;
                console.log('UI инициализирован');
            }

            setupEventListeners() {
                // Клик кнопка
                const clickButton = document.getElementById('clickButton');
                if (clickButton) {
                    clickButton.addEventListener('click', (e) => {
                        this.handleClick(e);
                    });
                    
                    // Поддержка горячих клавиш
                    document.addEventListener('keydown', (e) => {
                        if (e.code === 'Space' || e.code === 'Enter') {
                            e.preventDefault();
                            this.handleClick();
                        }
                    });
                }

                // Кнопки сохранения/загрузки
                document.getElementById('saveButton')?.addEventListener('click', () => {
                    this.game.saveGame();
                });

                document.getElementById('loadButton')?.addEventListener('click', () => {
                    this.game.loadGame();
                    this.updateAllUI();
                });

                document.getElementById('resetButton')?.addEventListener('click', () => {
                    if (this.game.resetGame()) {
                        this.updateAllUI();
                    }
                });

                document.getElementById('exportButton')?.addEventListener('click', () => {
                    this.game.exportSave();
                });

                document.getElementById('importButton')?.addEventListener('click', () => {
                    const input = document.createElement('input');
                    input.type = 'file';
                    input.accept = '.json';
                    input.onchange = (e) => {
                        const file = e.target.files[0];
                        const reader = new FileReader();
                        reader.onload = (event) => {
                            this.game.importSave(event.target.result);
                            this.updateAllUI();
                        };
                        reader.readAsText(file);
                    };
                    input.click();
                });

                // Кнопка престижа
                document.getElementById('prestigeButton')?.addEventListener('click', () => {
                    this.showPrestigeModal();
                });

                // Магазин престижа
                document.getElementById('prestigeShopButton')?.addEventListener('click', () => {
                    this.showPrestigeShop();
                });

                // Табы
                this.setupTabs();
                
                // Модальные окна
                this.setupModals();
            }

            setupTabs() {
                // Табы ресурсов
                const resourceTabs = document.querySelectorAll('#resourceTabs .tab');
                resourceTabs.forEach(tab => {
                    tab.addEventListener('click', () => {
                        const tabName = tab.dataset.tab;
                        this.switchTab('resourceTabs', tabName);
                    });
                });

                // Табы улучшений
                const upgradeTabs = document.querySelectorAll('#upgradeTabs .tab');
                upgradeTabs.forEach(tab => {
                    tab.addEventListener('click', () => {
                        const tabName = tab.dataset.tab;
                        this.switchTab('upgradeTabs', tabName);
                        this.updateUpgradesUI(tabName);
                    });
                });
            }

            setupModals() {
                // Закрытие модальных окон
                document.getElementById('closePrestigeModal')?.addEventListener('click', () => {
                    this.hideModal('prestigeModal');
                });

                document.getElementById('closeGalaxyModal')?.addEventListener('click', () => {
                    this.hideModal('galaxyModal');
                });

                // Закрытие по клику вне модального окна
                const modals = document.querySelectorAll('.modal');
                modals.forEach(modal => {
                    modal.addEventListener('click', (e) => {
                        if (e.target === modal) {
                            modal.classList.remove('show');
                        }
                    });
                });
            }

            switchTab(containerId, tabName) {
                const container = document.getElementById(containerId);
                if (!container) return;
                
                // Обновление активной вкладки
                const tabs = container.querySelectorAll('.tab');
                tabs.forEach(tab => {
                    tab.classList.remove('active');
                    if (tab.dataset.tab === tabName) {
                        tab.classList.add('active');
                    }
                });
                
                // Показ соответствующего контента
                const tabContents = container.parentElement.querySelectorAll('.tab-content');
                tabContents.forEach(content => {
                    content.classList.remove('active');
                    if (content.id === tabName + 'Resources' || content.id === tabName) {
                        content.classList.add('active');
                    }
                });
            }

            showModal(modalId) {
                const modal = document.getElementById(modalId);
                if (modal) {
                    modal.classList.add('show');
                    this.game.activeModals.push(modalId);
                }
            }

            hideModal(modalId) {
                const modal = document.getElementById(modalId);
                if (modal) {
                    modal.classList.remove('show');
                    const index = this.game.activeModals.indexOf(modalId);
                    if (index > -1) {
                        this.game.activeModals.splice(index, 1);
                    }
                }
            }

            // ===== ОБРАБОТКА КЛИКОВ =====
            handleClick(event = null) {
                const result = this.game.click();
                
                if (result) {
                    // Визуальный эффект
                    this.showClickEffect(result.energy, result.combo);
                    
                    // Обновление UI
                    this.updateMainStats();
                    
                    // Обновление комбо
                    if (result.combo > 1) {
                        this.showCombo(result.combo);
                    }
                }
            }

            showClickEffect(energy, combo) {
                const clickButton = document.getElementById('clickButton');
                if (!clickButton) return;
                
                // Создание текстового эффекта
                const effect = document.createElement('div');
                effect.className = 'click-multiplier';
                effect.textContent = `+${formatNumber(energy)}`;
                effect.style.color = combo > 3 ? '#ff4757' : '#fdcb6e';
                
                clickButton.appendChild(effect);
                
                // Удаление эффекта
                setTimeout(() => {
                    if (effect.parentNode === clickButton) {
                        clickButton.removeChild(effect);
                    }
                }, 1200);
                
                // Анимация кнопки
                if (this.game.settings.animations) {
                    clickButton.style.transform = 'scale(0.95)';
                    setTimeout(() => {
                        clickButton.style.transform = '';
                    }, 100);
                }
            }

            showCombo(combo) {
                // Можно добавить отображение комбо в интерфейсе
                if (combo > 3) {
                    this.game.showNotification(`Комбо x${combo}!`, 'warning');
                }
            }

            // ===== ИНИЦИАЛИЗАЦИЯ UI КОМПОНЕНТОВ =====
            initializeResourcesUI() {
                this.updateResourcesUI();
            }

            initializeUpgradesUI() {
                this.updateUpgradesUI('click');
            }

            initializeAutomationUI() {
                this.updateAutomationUI();
            }

            initializeAchievementsUI() {
                this.updateAchievementsUI();
            }

            initializeResearchUI() {
                this.updateResearchUI();
            }

            initializePrestigeUI() {
                this.updatePrestigeUI();
            }

            initializeCraftingUI() {
                this.updateCraftingUI();
            }

            initializeSettingsUI() {
                // Инициализация настроек
            }

            // ===== ОБНОВЛЕНИЕ UI =====
            updateAllUI() {
                this.updateMainStats();
                this.updateResourcesUI();
                this.updateUpgradesUI();
                this.updateAutomationUI();
                this.updateAchievementsUI();
                this.updateResearchUI();
                this.updatePrestigeUI();
                this.updateCraftingUI();
            }

            updateMainStats() {
                // Энергия
                const energyEl = document.getElementById('energy');
                if (energyEl) {
                    energyEl.textContent = formatNumber(this.game.resources.energy.value);
                }
                
                // ЭПС
                const epsEl = document.getElementById('eps');
                if (epsEl) {
                    epsEl.textContent = formatNumber(this.game.getEnergyPerSecond()) + '/сек';
                }
                
                // Уровень
                const levelEl = document.getElementById('level');
                if (levelEl) {
                    levelEl.textContent = this.game.level.toString();
                }
                
                // Престиж
                const prestigeEl = document.getElementById('prestige');
                if (prestigeEl) {
                    prestigeEl.textContent = this.game.prestigeLevel.toString();
                }
                
                // Мультипликатор
                const multiplierEl = document.getElementById('multiplier');
                if (multiplierEl) {
                    multiplierEl.textContent = formatNumber(this.game.getGlobalMultiplier()) + 'x';
                }
                
                // Мощность клика
                const clickPowerEl = document.getElementById('clickPower');
                if (clickPowerEl) {
                    clickPowerEl.textContent = `+${formatNumber(this.game.getClickPower())} за клик`;
                }
                
                // Прогресс уровня
                const levelProgressEl = document.getElementById('levelProgress');
                const levelProgressTextEl = document.getElementById('levelProgressText');
                if (levelProgressEl && levelProgressTextEl) {
                    const percent = this.game.getLevelProgressPercent();
                    levelProgressEl.style.width = `${percent}%`;
                    levelProgressTextEl.textContent = `${percent.toFixed(1)}%`;
                }
            }

            updateResourcesUI() {
                const basicGrid = document.getElementById('basicResources');
                const advancedGrid = document.getElementById('advancedResources');
                const exoticGrid = document.getElementById('exoticResources');
                
                if (!basicGrid || !advancedGrid || !exoticGrid) return;
                
                // Очистка
                basicGrid.innerHTML = '';
                advancedGrid.innerHTML = '';
                exoticGrid.innerHTML = '';
                
                // Определение категорий ресурсов
                const basicResources = ['energy', 'metal', 'crystals', 'uranium'];
                const advancedResources = ['antimatter', 'darkMatter', 'quantum', 'science'];
                const exoticResources = ['technology', 'galactic', 'prestige', 'nebula', 'singularity', 'multiverse'];
                
                // Создание элементов ресурсов
                for (const [id, resource] of Object.entries(this.game.resources)) {
                    if (!resource.unlocked && resource.value === 0) continue;
                    
                    const resourceEl = this.createResourceElement(resource);
                    
                    if (basicResources.includes(id)) {
                        basicGrid.appendChild(resourceEl);
                    } else if (advancedResources.includes(id)) {
                        advancedGrid.appendChild(resourceEl);
                    } else if (exoticResources.includes(id)) {
                        exoticGrid.appendChild(resourceEl);
                    }
                }
            }

            createResourceElement(resource) {
                const div = document.createElement('div');
                div.className = 'resource-item';
                div.innerHTML = `
                    <div class="resource-icon">
                        <i class="${resource.icon}"></i>
                    </div>
                    <div class="resource-name">${resource.name}</div>
                    <div class="resource-value">${resource.formatValue()}</div>
                    ${resource.perSecond > 0 ? 
                        `<div class="resource-per-second">${resource.formatPerSecond()}</div>` : 
                        ''
                    }
                `;
                
                // Анимация при изменении значения
                let lastValue = resource.value;
                const valueEl = div.querySelector('.resource-value');
                
                const observer = setInterval(() => {
                    if (resource.value !== lastValue) {
                        lastValue = resource.value;
                        if (valueEl) {
                            valueEl.textContent = resource.formatValue();
                            
                            // Эффект обновления
                            if (this.game.settings.animations) {
                                valueEl.style.transform = 'scale(1.1)';
                                setTimeout(() => {
                                    valueEl.style.transform = 'scale(1)';
                                }, 200);
                            }
                        }
                    }
                }, 100);
                
                // Очистка при удалении элемента
                div.dataset.observerId = observer;
                
                return div;
            }

            updateUpgradesUI(category = 'click') {
                const container = document.getElementById('upgradesList');
                if (!container) return;
                
                container.innerHTML = '';
                
                // Фильтрация улучшений по категории
                const upgrades = this.game.upgrades.filter(upgrade => 
                    upgrade.category === category && (upgrade.unlocked || upgrade.level > 0)
                );
                
                if (upgrades.length === 0) {
                    container.innerHTML = '<div style="text-align: center; padding: 20px; color: var(--secondary);">Улучшения будут доступны позже</div>';
                    return;
                }
                
                // Создание элементов улучшений
                for (const upgrade of upgrades) {
                    const upgradeEl = this.createUpgradeElement(upgrade);
                    container.appendChild(upgradeEl);
                }
            }

            createUpgradeElement(upgrade) {
                const div = document.createElement('div');
                
                let className = 'upgrade-item';
                if (upgrade.purchased) className += ' purchased';
                if (upgrade.isMaxLevel()) className += ' max-level';
                
                div.className = className;
                
                // Эффект улучшения
                let effectText = '';
                switch (upgrade.effect.type) {
                    case 'clickPower':
                        effectText = `+${formatNumber(upgrade.getEffectValue())} за клик`;
                        break;
                    case 'energyPerSecond':
                        effectText = `+${formatNumber(upgrade.getEffectValue())} энергии/сек`;
                        break;
                    case 'globalMultiplier':
                        effectText = `+${(upgrade.getEffectValue() * 100).toFixed(1)}% ко всем ресурсам`;
                        break;
                    case 'autoClick':
                        effectText = `${upgrade.getEffectValue()} авто-клик/сек`;
                        break;
                    case 'quantumBonus':
                        effectText = `${(upgrade.getEffectValue() * 100).toFixed(1)}% шанс удвоить клик`;
                        break;
                }
                
                div.innerHTML = `
                    <div class="upgrade-header">
                        <div class="upgrade-name">
                            <i class="fas fa-arrow-up"></i>
                            ${upgrade.name}
                            ${upgrade.maxLevel > 1 ? `<span class="upgrade-level">Ур. ${upgrade.level}/${upgrade.maxLevel}</span>` : ''}
                        </div>
                        <div class="upgrade-cost">
                            ${upgrade.isMaxLevel() ? 'МАКС.' : formatNumber(upgrade.getNextCost()) + ' энергии'}
                        </div>
                    </div>
                    <div class="upgrade-description">${upgrade.description}</div>
                    <div class="upgrade-effect">
                        <span>${effectText}</span>
                        ${upgrade.isMaxLevel() ? 
                            '<span><i class="fas fa-trophy"></i> Макс. уровень</span>' : 
                            upgrade.purchased ? '<span><i class="fas fa-check"></i> Куплено</span>' : ''
                        }
                    </div>
                    ${upgrade.maxLevel > 1 ? `
                        <div class="upgrade-progress">
                            <div class="upgrade-progress-bar" style="width: ${(upgrade.level / upgrade.maxLevel) * 100}%"></div>
                        </div>
                    ` : ''}
                `;
                
                // Обработчик клика
                if (!upgrade.isMaxLevel() && upgrade.canPurchase(this.game.resources)) {
                    div.style.cursor = 'pointer';
                    div.addEventListener('click', () => {
                        this.purchaseUpgrade(upgrade);
                    });
                } else {
                    div.style.cursor = 'not-allowed';
                }
                
                return div;
            }

            purchaseUpgrade(upgrade) {
                if (!upgrade.canPurchase(this.game.resources)) return;
                
                if (this.game.resources.energy.subtract(upgrade.getNextCost())) {
                    upgrade.purchase();
                    this.game.stats.upgradesBought++;
                    
                    // Применение эффекта
                    this.applyUpgradeEffect(upgrade);
                    
                    // Обновление UI
                    this.updateMainStats();
                    this.updateUpgradesUI(upgrade.category);
                    
                    this.game.showNotification(`Улучшение "${upgrade.name}" куплено!`, 'success');
                    
                    // Проверка достижений
                    this.game.checkAchievements();
                }
            }

            applyUpgradeEffect(upgrade) {
                // Эффекты применяются автоматически при расчетах в игровой логике
            }

            updateAutomationUI() {
                const container = document.getElementById('automationGrid');
                if (!container) return;
                
                container.innerHTML = '';
                
                for (const automation of this.game.automations) {
                    if (!automation.unlocked && automation.count === 0) continue;
                    
                    const autoEl = this.createAutomationElement(automation);
                    container.appendChild(autoEl);
                }
            }

            createAutomationElement(automation) {
                const div = document.createElement('div');
                div.className = 'resource-item';
                
                const resource = this.game.resources[automation.resourceId];
                const canPurchase = automation.canPurchase(this.game.resources);
                
                div.innerHTML = `
                    <div class="resource-icon">
                        <i class="fas fa-robot"></i>
                    </div>
                    <div class="resource-name">${automation.name}</div>
                    <div class="resource-value">${automation.count}</div>
                    <div class="resource-per-second">+${formatNumber(automation.getTotalProduction())}/сек</div>
                    <div style="margin-top: 10px;">
                        <button class="btn ${canPurchase ? 'btn-success' : 'btn'}" 
                                style="font-size: 0.9rem; padding: 8px 15px;"
                                ${canPurchase ? '' : 'disabled'}>
                            Купить (${formatNumber(automation.cost)} энергии)
                        </button>
                    </div>
                `;
                
                const button = div.querySelector('button');
                if (button && canPurchase) {
                    button.addEventListener('click', () => {
                        this.purchaseAutomation(automation);
                    });
                }
                
                return div;
            }

            purchaseAutomation(automation) {
                if (automation.purchase(this.game.resources)) {
                    this.game.stats.automationsBought++;
                    
                    // Обновление UI
                    this.updateMainStats();
                    this.updateAutomationUI();
                    
                    this.game.showNotification(`${automation.name} куплен!`, 'success');
                    
                    // Проверка достижений
                    this.game.checkAchievements();
                }
            }

            updateAchievementsUI() {
                const container = document.getElementById('achievementsGrid');
                if (!container) return;
                
                container.innerHTML = '';
                
                for (const achievement of this.game.achievements) {
                    const achEl = this.createAchievementElement(achievement);
                    container.appendChild(achEl);
                }
            }

            createAchievementElement(achievement) {
                const div = document.createElement('div');
                div.className = `achievement ${achievement.unlocked ? 'unlocked' : ''}`;
                
                const progress = achievement.getProgressPercent();
                
                div.innerHTML = `
                    <div class="achievement-icon">
                        <i class="${achievement.icon}"></i>
                    </div>
                    <div class="achievement-name">${achievement.name}</div>
                    <div class="achievement-description">${achievement.description}</div>
                    ${!achievement.unlocked ? `
                        <div class="achievement-progress">
                            <div class="achievement-progress-bar" style="width: ${progress}%"></div>
                        </div>
                        <div style="text-align: center; margin-top: 5px; font-size: 0.8rem; color: var(--secondary);">
                            ${achievement.maxProgress > 1 ? 
                                `${formatNumber(achievement.progress)}/${formatNumber(achievement.maxProgress)}` : 
                                'В процессе...'
                            }
                        </div>
                    ` : ''}
                `;
                
                return div;
            }

            updateResearchUI() {
                const container = document.getElementById('researchTree');
                if (!container) return;
                
                container.innerHTML = '';
                
                for (const research of this.game.researches) {
                    const researchEl = this.createResearchElement(research);
                    container.appendChild(researchEl);
                }
            }

            createResearchElement(research) {
                const div = document.createElement('div');
                div.className = `resource-item ${research.completed ? 'unlocked' : research.inProgress ? 'in-progress' : 'locked'}`;
                
                let statusText = '';
                let buttonText = '';
                let buttonClass = 'btn';
                let disabled = false;
                
                if (research.completed) {
                    statusText = '<span style="color: var(--success);"><i class="fas fa-check"></i> Завершено</span>';
                } else if (research.inProgress) {
                    const progress = research.getProgressPercent();
                    statusText = `Исследование: ${progress.toFixed(1)}%`;
                    buttonText = 'В процессе...';
                    buttonClass = 'btn-info';
                    disabled = true;
                } else {
                    statusText = research.canStart(this.game) ? 
                        `Стоимость: ${formatNumber(research.cost)} науки` :
                        'Недоступно';
                    buttonText = 'Начать исследование';
                    buttonClass = research.canStart(this.game) ? 'btn-success' : 'btn';
                    disabled = !research.canStart(this.game);
                }
                
                div.innerHTML = `
                    <div class="resource-icon">
                        <i class="${research.icon}"></i>
                    </div>
                    <div class="resource-name">${research.name}</div>
                    <div class="resource-description" style="font-size: 0.9rem; margin: 10px 0; color: #bdc3c7;">
                        ${research.description}
                    </div>
                    <div style="margin: 10px 0; color: var(--info);">
                        ${statusText}
                    </div>
                    ${research.inProgress ? `
                        <div class="progress-bar" style="height: 10px;">
                            <div class="progress-fill" style="width: ${research.getProgressPercent()}%"></div>
                        </div>
                    ` : ''}
                    ${!research.completed ? `
                        <div style="margin-top: 10px;">
                            <button class="${buttonClass}" 
                                    style="font-size: 0.9rem; padding: 8px 15px;"
                                    ${disabled ? 'disabled' : ''}>
                                ${buttonText}
                            </button>
                        </div>
                    ` : ''}
                `;
                
                const button = div.querySelector('button');
                if (button && !disabled && !research.completed && !research.inProgress) {
                    button.addEventListener('click', () => {
                        this.startResearch(research);
                    });
                }
                
                return div;
            }

            startResearch(research) {
                if (research.start(this.game)) {
                    this.game.stats.researchesCompleted++;
                    
                    // Обновление UI
                    this.updateResearchUI();
                    
                    this.game.showNotification(`Исследование "${research.name}" начато!`, 'info');
                }
            }

            updatePrestigeUI() {
                const pointsEl = document.getElementById('prestigePoints');
                const multiplierEl = document.getElementById('prestigeMultiplier');
                
                if (pointsEl) {
                    pointsEl.textContent = formatNumber(this.game.prestigePoints);
                }
                
                if (multiplierEl) {
                    multiplierEl.textContent = formatNumber(this.game.multipliers.prestige) + 'x';
                }
            }

            updateCraftingUI() {
                const container = document.getElementById('craftingRecipes');
                if (!container) return;
                
                container.innerHTML = '<div style="text-align: center; padding: 20px; color: var(--secondary);">Система крафтинга будет добавлена в будущем обновлении</div>';
            }

            // ===== МОДАЛЬНЫЕ ОКНА =====
            showPrestigeModal() {
                const modalContent = document.getElementById('prestigeModalContent');
                if (!modalContent) return;
                
                const requiredEnergy = 1000000;
                const currentEnergy = this.game.resources.energy.total;
                const prestigePoints = Math.floor(Math.sqrt(currentEnergy / 1e6) * 10);
                const canPrestige = currentEnergy >= requiredEnergy;
                
                modalContent.innerHTML = `
                    <div style="text-align: center; margin-bottom: 30px;">
                        <div style="font-size: 1.2rem; margin-bottom: 20px; color: var(--secondary);">
                            Престижное перерождение позволяет начать игру заново с бонусами
                        </div>
                        
                        <div style="background: rgba(0, 0, 0, 0.3); padding: 20px; border-radius: 15px; margin-bottom: 20px;">
                            <div style="display: flex; justify-content: space-between; margin-bottom: 10px;">
                                <span>Накоплено энергии:</span>
                                <span class="stat-value" style="font-size: 1.2rem;">${formatNumber(currentEnergy)}</span>
                            </div>
                            <div style="display: flex; justify-content: space-between; margin-bottom: 10px;">
                                <span>Требуется для престижа:</span>
                                <span class="stat-value" style="font-size: 1.2rem; color: ${canPrestige ? 'var(--success)' : 'var(--danger)'}">
                                    ${formatNumber(requiredEnergy)}
                                </span>
                            </div>
                            <div style="display: flex; justify-content: space-between;">
                                <span>Получено очков престижа:</span>
                                <span class="stat-value" style="font-size: 1.2rem; color: var(--star-gold);">
                                    ${prestigePoints}
                                </span>
                            </div>
                        </div>
                        
                        <div style="margin-bottom: 30px;">
                            <h3 style="color: var(--cyber-blue); margin-bottom: 15px;">Что будет сброшено:</h3>
                            <ul style="text-align: left; padding-left: 20px; color: #bdc3c7;">
                                <li>Все ресурсы (кроме очков престижа)</li>
                                <li>Все улучшения</li>
                                <li>Вся автоматизация</li>
                                <li>Исследования</li>
                                <li>Уровень и опыт</li>
                            </ul>
                        </div>
                        
                        <div style="margin-bottom: 30px;">
                            <h3 style="color: var(--cyber-blue); margin-bottom: 15px;">Что сохранится:</h3>
                            <ul style="text-align: left; padding-left: 20px; color: #bdc3c7;">
                                <li>Очки престижа</li>
                                <li>Уровень престижа</li>
                                <li>Престижные улучшения</li>
                                <li>Достижения (частично)</li>
                            </ul>
                        </div>
                        
                        <button class="btn ${canPrestige ? 'btn-warning' : 'btn'}" 
                                id="confirmPrestige"
                                style="font-size: 1.2rem; padding: 15px 40px;"
                                ${canPrestige ? '' : 'disabled'}>
                            <i class="fas fa-redo"></i> ВЫПОЛНИТЬ ПРЕСТИЖ
                        </button>
                        
                        ${!canPrestige ? 
                            `<div style="margin-top: 15px; color: var(--danger);">
                                Недостаточно энергии для престижа
                            </div>` : 
                            ''
                        }
                    </div>
                `;
                
                const confirmBtn = document.getElementById('confirmPrestige');
                if (confirmBtn && canPrestige) {
                    confirmBtn.addEventListener('click', () => {
                        if (this.game.prestige()) {
                            this.updateAllUI();
                            this.hideModal('prestigeModal');
                        }
                    });
                }
                
                this.showModal('prestigeModal');
            }

            showPrestigeShop() {
                // Реализация магазина престижа
                this.game.showNotification('Магазин престижа будет добавлен в будущем обновлении', 'info');
            }

            // ===== ИГРОВОЙ ЦИКЛ UI =====
            startUILoop() {
                this.updateInterval = setInterval(() => {
                    this.updateMainStats();
                }, 100);
            }

            stopUILoop() {
                if (this.updateInterval) {
                    clearInterval(this.updateInterval);
                    this.updateInterval = null;
                }
            }
        }

        // ===== ИНИЦИАЛИЗАЦИЯ ИГРЫ =====
        let game;
        let gameUI;

        function initializeGame() {
            console.log('Запуск игры...');
            
            // Создание экземпляра игры
            game = new SpaceClickerGame();
            
            // Создание UI
            gameUI = new GameUI(game);
            
            // Загрузка сохранения
            const saveLoaded = game.loadGame();
            
            // Инициализация UI
            gameUI.initialize();
            
            // Запуск игрового цикла
            game.startGameLoop();
            
            // Автосохранение при закрытии вкладки
            window.addEventListener('beforeunload', () => {
                game.saveGame();
            });
            
            // Периодическое автосохранение
            setInterval(() => {
                if (game.settings.autoSave) {
                    game.saveGame();
                }
            }, CONFIG.AUTOSAVE_INTERVAL);
            
            console.log('Игра запущена!');
            
            // Показать приветственное сообщение
            setTimeout(() => {
                if (!saveLoaded) {
                    game.showNotification('Добро пожаловать в Космический Кликер: Эра Восхождения! Кликайте по центральной кнопке для генерации энергии.', 'info');
                }
            }, 2000);
        }

        // Запуск игры после загрузки страницы
        document.addEventListener('DOMContentLoaded', initializeGame);

        // Экспорт для отладки
        window.getGame = () => game;
        window.getGameUI = () => gameUI;
        window.formatNumber = formatNumber;

        console.log('Инициализация завершена!');
    </script>
</body>
</html>
