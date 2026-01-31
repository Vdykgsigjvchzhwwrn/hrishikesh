<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Secure Authentication System</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #0c2461, #1e3799);
            color: #333;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .container {
            width: 100%;
            max-width: 450px;
            background-color: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(to right, #1e3c72, #2a5298);
            color: white;
            padding: 25px;
            text-align: center;
        }

        .header h1 {
            font-size: 1.8rem;
            margin-bottom: 5px;
        }

        .header p {
            opacity: 0.9;
            font-size: 0.9rem;
        }

        .tabs {
            display: flex;
            background-color: #f8f9fa;
            border-bottom: 1px solid #dee2e6;
        }

        .tab {
            flex: 1;
            text-align: center;
            padding: 15px;
            cursor: pointer;
            font-weight: 600;
            color: #495057;
            transition: all 0.3s;
        }

        .tab.active {
            color: #1e3c72;
            border-bottom: 3px solid #1e3c72;
            background-color: white;
        }

        .form-container {
            padding: 30px;
        }

        .form {
            display: none;
        }

        .form.active {
            display: block;
        }

        .input-group {
            margin-bottom: 20px;
            position: relative;
        }

        .input-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #495057;
        }

        .input-group input {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #dee2e6;
            border-radius: 8px;
            font-size: 1rem;
            transition: border-color 0.3s;
        }

        .input-group input:focus {
            border-color: #1e3c72;
            outline: none;
        }

        .input-group .icon {
            position: absolute;
            right: 15px;
            top: 40px;
            color: #6c757d;
        }

        .btn {
            width: 100%;
            padding: 14px;
            background: linear-gradient(to right, #1e3c72, #2a5298);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            margin-top: 10px;
        }

        .btn:hover {
            background: linear-gradient(to right, #2a5298, #3b6cb7);
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }

        .btn:active {
            transform: translateY(0);
        }

        .btn-secondary {
            background: #6c757d;
        }

        .btn-secondary:hover {
            background: #5a6268;
        }

        .security-info {
            background-color: #f8f9fa;
            padding: 15px;
            border-radius: 8px;
            margin-top: 25px;
            border-left: 4px solid #1e3c72;
        }

        .security-info h3 {
            color: #1e3c72;
            margin-bottom: 10px;
            font-size: 1.1rem;
        }

        .security-info ul {
            padding-left: 20px;
            font-size: 0.9rem;
            color: #495057;
        }

        .security-info li {
            margin-bottom: 8px;
        }

        .otp-container {
            display: flex;
            justify-content: space-between;
            margin-top: 10px;
        }

        .otp-input {
            width: 50px;
            height: 60px;
            text-align: center;
            font-size: 1.5rem;
            border: 2px solid #dee2e6;
            border-radius: 8px;
        }

        .biometric-options {
            display: flex;
            justify-content: space-around;
            margin: 20px 0;
        }

        .biometric-option {
            text-align: center;
            padding: 15px;
            border: 2px solid #dee2e6;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s;
            flex: 1;
            margin: 0 5px;
        }

        .biometric-option:hover {
            border-color: #1e3c72;
            background-color: #f8f9fa;
        }

        .biometric-option i {
            font-size: 2rem;
            color: #1e3c72;
            margin-bottom: 10px;
        }

        .status-message {
            padding: 12px;
            border-radius: 8px;
            margin: 15px 0;
            text-align: center;
            display: none;
        }

        .success {
            background-color: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
            display: block;
        }

        .error {
            background-color: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
            display: block;
        }

        .info {
            background-color: #d1ecf1;
            color: #0c5460;
            border: 1px solid #bee5eb;
            display: block;
        }

        .footer {
            text-align: center;
            padding: 20px;
            color: #6c757d;
            font-size: 0.9rem;
            border-top: 1px solid #dee2e6;
        }

        .footer a {
            color: #1e3c72;
            text-decoration: none;
        }

        .verification-step {
            display: none;
        }

        .verification-step.active {
            display: block;
        }

        .loader {
            display: none;
            border: 4px solid #f3f3f3;
            border-top: 4px solid #1e3c72;
            border-radius: 50%;
            width: 30px;
            height: 30px;
            animation: spin 1s linear infinite;
            margin: 0 auto;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        @media (max-width: 500px) {
            .container {
                max-width: 100%;
            }
            
            .biometric-options {
                flex-direction: column;
            }
            
            .biometric-option {
                margin: 5px 0;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-shield-alt"></i> Secure Authentication System</h1>
            <p>Multi-factor authentication for enhanced security</p>
        </div>
        
        <div class="tabs">
            <div class="tab active" data-tab="login">Login</div>
            <div class="tab" data-tab="register">Register</div>
            <div class="tab" data-tab="security">Security Info</div>
        </div>
        
        <div class="form-container">
            <!-- Login Form -->
            <div id="login-form" class="form active">
                <div id="login-step1" class="verification-step active">
                    <h2>Login to Your Account</h2>
                    <p style="margin-bottom: 20px; color: #6c757d;">Enter your credentials to continue</p>
                    
                    <div id="login-message" class="status-message"></div>
                    
                    <div class="input-group">
                        <label for="login-username"><i class="fas fa-user"></i> Username or Email</label>
                        <input type="text" id="login-username" placeholder="Enter your username or email">
                        <span class="icon"><i class="fas fa-user"></i></span>
                    </div>
                    
                    <div class="input-group">
                        <label for="login-password"><i class="fas fa-lock"></i> Password</label>
                        <input type="password" id="login-password" placeholder="Enter your password">
                        <span class="icon"><i class="fas fa-lock"></i></span>
                    </div>
                    
                    <button id="login-btn" class="btn">Continue to Verification</button>
                    
                    <div class="security-info">
                        <h3><i class="fas fa-info-circle"></i> Login Security Tips</h3>
                        <ul>
                            <li>Use a strong, unique password</li>
                            <li>Never share your credentials with anyone</li>
                            <li>Ensure you're on a secure connection</li>
                        </ul>
                    </div>
                </div>
                
                <!-- OTP Verification Step -->
                <div id="login-step2" class="verification-step">
                    <h2>Two-Factor Verification</h2>
                    <p style="margin-bottom: 20px; color: #6c757d;">Enter the 6-digit code sent to your registered email</p>
                    
                    <div class="otp-container">
                        <input type="text" class="otp-input" maxlength="1" data-index="1">
                        <input type="text" class="otp-input" maxlength="1" data-index="2">
                        <input type="text" class="otp-input" maxlength="1" data-index="3">
                        <input type="text" class="otp-input" maxlength="1" data-index="4">
                        <input type="text" class="otp-input" maxlength="1" data-index="5">
                        <input type="text" class="otp-input" maxlength="1" data-index="6">
                    </div>
                    
                    <p style="text-align: center; margin: 15px 0; font-size: 0.9rem;">
                        Didn't receive code? <a href="#" id="resend-otp">Resend</a>
                    </p>
                    
                    <button id="verify-otp-btn" class="btn">Verify OTP</button>
                    <button id="back-to-login" class="btn btn-secondary">Back to Login</button>
                    
                    <div class="security-info">
                        <h3><i class="fas fa-shield-alt"></i> Biometric Authentication</h3>
                        <p style="margin-bottom: 10px;">Alternatively, use biometric verification</p>
                        <div class="biometric-options">
                            <div class="biometric-option" id="fingerprint-auth">
                                <i class="fas fa-fingerprint"></i>
                                <p>Fingerprint</p>
                            </div>
                            <div class="biometric-option" id="face-auth">
                                <i class="fas fa-user-check"></i>
                                <p>Face ID</p>
                            </div>
                        </div>
                    </div>
                </div>
                
                <!-- Successful Login Step -->
                <div id="login-success" class="verification-step">
                    <div class="status-message success">
                        <h3><i class="fas fa-check-circle"></i> Authentication Successful!</h3>
                        <p>You have been securely logged in.</p>
                    </div>
                    
                    <div class="security-info">
                        <h3><i class="fas fa-history"></i> Recent Login Activity</h3>
                        <ul>
                            <li><strong>Current Login:</strong> Just now from this device</li>
                            <li><strong>Previous Login:</strong> Yesterday from Chrome on Windows</li>
                            <li><strong>Location:</strong> Verified (matches your usual pattern)</li>
                        </ul>
                    </div>
                    
                    <button id="logout-btn" class="btn">Logout</button>
                </div>
            </div>
            
            <!-- Registration Form -->
            <div id="register-form" class="form">
                <h2>Create New Account</h2>
                <p style="margin-bottom: 20px; color: #6c757d;">Register for a secure account with multi-factor authentication</p>
                
                <div id="register-message" class="status-message"></div>
                
                <div class="input-group">
                    <label for="register-username"><i class="fas fa-user"></i> Username</label>
                    <input type="text" id="register-username" placeholder="Choose a username">
                    <span class="icon"><i class="fas fa-user"></i></span>
                </div>
                
                <div class="input-group">
                    <label for="register-email"><i class="fas fa-envelope"></i> Email Address</label>
                    <input type="email" id="register-email" placeholder="Enter your email">
                    <span class="icon"><i class="fas fa-envelope"></i></span>
                </div>
                
                <div class="input-group">
                    <label for="register-password"><i class="fas fa-lock"></i> Password</label>
                    <input type="password" id="register-password" placeholder="Create a strong password">
                    <span class="icon"><i class="fas fa-lock"></i></span>
                </div>
                
                <div class="input-group">
                    <label for="confirm-password"><i class="fas fa-lock"></i> Confirm Password</label>
                    <input type="password" id="confirm-password" placeholder="Confirm your password">
                    <span class="icon"><i class="fas fa-lock"></i></span>
                </div>
                
                <div class="input-group">
                    <label>
                        <input type="checkbox" id="enable-2fa"> Enable Two-Factor Authentication (Recommended)
                    </label>
                </div>
                
                <div class="input-group">
                    <label>
                        <input type="checkbox" id="enable-biometric"> Enable Biometric Authentication (Fingerprint/Face ID)
                    </label>
                </div>
                
                <button id="register-btn" class="btn">Create Account</button>
                
                <div class="security-info">
                    <h3><i class="fas fa-lock"></i> Password Requirements</h3>
                    <ul>
                        <li>At least 8 characters long</li>
                        <li>Contains uppercase and lowercase letters</li>
                        <li>Includes at least one number and special character</li>
                        <li>Not based on personal information</li>
                    </ul>
                </div>
            </div>
            
            <!-- Security Information -->
            <div id="security-info" class="form">
                <h2>Security Information</h2>
                
                <div class="security-info">
                    <h3><i class="fas fa-shield-alt"></i> Multi-Factor Authentication (MFA)</h3>
                    <p>MFA adds an extra layer of security by requiring two or more verification factors:</p>
                    <ul>
                        <li><strong>Something you know:</strong> Password or PIN</li>
                        <li><strong>Something you have:</strong> Phone (for OTP) or Security key</li>
                        <li><strong>Something you are:</strong> Biometric (Fingerprint, Face ID)</li>
                    </ul>
                </div>
                
                <div class="security-info">
                    <h3><i class="fas fa-mobile-alt"></i> One-Time Password (OTP)</h3>
                    <p>OTP is a dynamically generated code valid for a single login session. It prevents replay attacks even if your password is compromised.</p>
                </div>
                
                <div class="security-info">
                    <h3><i class="fas fa-fingerprint"></i> Biometric Authentication</h3>
                    <p>Biometric authentication uses unique biological characteristics for verification. It's convenient and difficult to forge.</p>
                </div>
                
                <div class="security-info">
                    <h3><i class="fas fa-user-secret"></i> Best Practices</h3>
                    <ul>
                        <li>Always enable MFA when available</li>
                        <li>Use a password manager to generate and store strong passwords</li>
                        <li>Regularly update your passwords and security settings</li>
                        <li>Be cautious of phishing attempts and suspicious links</li>
                    </ul>
                </div>
            </div>
        </div>
        
        <div class="footer">
            <p>Secure Authentication System &copy; 2026 | <a href="#">Privacy Policy</a> | <a href="#">Terms of Service</a></p>
            <p><i class="fas fa-lock"></i> All connections are encrypted with TLS 1.3</p>
        </div>
    </div>
    
    <script>
        // DOM Elements
        const tabs = document.querySelectorAll('.tab');
        const forms = document.querySelectorAll('.form');
        const loginForm = document.getElementById('login-form');
        const registerForm = document.getElementById('register-form');
        const securityInfo = document.getElementById('security-info');
        
        // Login elements
        const loginStep1 = document.getElementById('login-step1');
        const loginStep2 = document.getElementById('login-step2');
        const loginSuccess = document.getElementById('login-success');
        const loginBtn = document.getElementById('login-btn');
        const verifyOtpBtn = document.getElementById('verify-otp-btn');
        const backToLoginBtn = document.getElementById('back-to-login');
        const logoutBtn = document.getElementById('logout-btn');
        const resendOtpLink = document.getElementById('resend-otp');
        const loginMessage = document.getElementById('login-message');
        const otpInputs = document.querySelectorAll('.otp-input');
        
        // Register elements
        const registerBtn = document.getElementById('register-btn');
        const registerMessage = document.getElementById('register-message');
        
        // Biometric elements
        const fingerprintAuth = document.getElementById('fingerprint-auth');
        const faceAuth = document.getElementById('face-auth');
        
        // Tab switching
        tabs.forEach(tab => {
            tab.addEventListener('click', () => {
                const tabId = tab.getAttribute('data-tab');
                
                // Update active tab
                tabs.forEach(t => t.classList.remove('active'));
                tab.classList.add('active');
                
                // Show corresponding form
                forms.forEach(form => form.classList.remove('active'));
                document.getElementById(`${tabId}-form`).classList.add('active');
                
                // Reset login steps
                if (tabId === 'login') {
                    resetLoginSteps();
                }
            });
        });
        
        // OTP input handling
        otpInputs.forEach(input => {
            input.addEventListener('input', (e) => {
                // Move to next input if current one is filled
                if (e.target.value.length === 1) {
                    const nextIndex = parseInt(e.target.getAttribute('data-index')) + 1;
                    const nextInput = document.querySelector(`.otp-input[data-index="${nextIndex}"]`);
                    if (nextInput) nextInput.focus();
                }
            });
            
            input.addEventListener('keydown', (e) => {
                // Move to previous input on backspace if current input is empty
                if (e.key === 'Backspace' && e.target.value === '') {
                    const prevIndex = parseInt(e.target.getAttribute('data-index')) - 1;
                    const prevInput = document.querySelector(`.otp-input[data-index="${prevIndex}"]`);
                    if (prevInput) prevInput.focus();
                }
            });
        });
        
        // Login process
        loginBtn.addEventListener('click', () => {
            const username = document.getElementById('login-username').value;
            const password = document.getElementById('login-password').value;
            
            if (!username || !password) {
                showMessage(loginMessage, 'Please enter both username and password', 'error');
                return;
            }
            
            // Simulate authentication
            showMessage(loginMessage, 'Verifying credentials...', 'info');
            
            // Simulate API call delay
            setTimeout(() => {
                // For demo purposes, accept any non-empty credentials
                showMessage(loginMessage, 'Credentials verified! Proceeding to two-factor authentication.', 'success');
                
                // Move to OTP step
                loginStep1.classList.remove('active');
                loginStep2.classList.add('active');
                
                // Generate and "send" OTP (for demo, we'll just show it)
                const otp = generateOTP();
                console.log(`Demo OTP: ${otp}`); // In real app, this would be sent via email/SMS
                
                // Auto-fill OTP for demo purposes
                setTimeout(() => {
                    otpInputs.forEach((input, index) => {
                        input.value = otp.charAt(index);
                    });
                }, 500);
            }, 1500);
        });
        
        // OTP Verification
        verifyOtpBtn.addEventListener('click', () => {
            let otp = '';
            otpInputs.forEach(input => {
                otp += input.value;
            });
            
            if (otp.length !== 6) {
                showMessage(loginMessage, 'Please enter the complete 6-digit OTP', 'error');
                return;
            }
            
            // Show loading
            verifyOtpBtn.innerHTML = '<div class="loader"></div>';
            
            // Simulate OTP verification
            setTimeout(() => {
                // For demo, accept any 6-digit OTP
                loginStep2.classList.remove('active');
                loginSuccess.classList.add('active');
                verifyOtpBtn.innerHTML = 'Verify OTP';
            }, 1500);
        });
        
        // Back to login button
        backToLoginBtn.addEventListener('click', resetLoginSteps);
        
        // Logout button
        logoutBtn.addEventListener('click', resetLoginSteps);
        
        // Resend OTP
        resendOtpLink.addEventListener('click', (e) => {
            e.preventDefault();
            
            // Generate new OTP
            const otp = generateOTP();
            console.log(`New demo OTP: ${otp}`); // In real app, this would be sent via email/SMS
            
            // Clear OTP inputs
            otpInputs.forEach(input => {
                input.value = '';
            });
            
            // Focus on first OTP input
            otpInputs[0].focus();
            
            // Show message
            showMessage(loginMessage, 'New OTP has been sent to your registered email', 'info');
        });
        
        // Biometric authentication simulation
        fingerprintAuth.addEventListener('click', () => {
            simulateBiometricAuth('fingerprint');
        });
        
        faceAuth.addEventListener('click', () => {
            simulateBiometricAuth('face');
        });
        
        // Registration process
        registerBtn.addEventListener('click', () => {
            const username = document.getElementById('register-username').value;
            const email = document.getElementById('register-email').value;
            const password = document.getElementById('register-password').value;
            const confirmPassword = document.getElementById('confirm-password').value;
            const enable2FA = document.getElementById('enable-2fa').checked;
            const enableBiometric = document.getElementById('enable-biometric').checked;
            
            // Validation
            if (!username || !email || !password || !confirmPassword) {
                showMessage(registerMessage, 'Please fill in all fields', 'error');
                return;
            }
            
            if (password !== confirmPassword) {
                showMessage(registerMessage, 'Passwords do not match', 'error');
                return;
            }
            
            if (password.length < 8) {
                showMessage(registerMessage, 'Password must be at least 8 characters long', 'error');
                return;
            }
            
            // Show loading
            registerBtn.innerHTML = '<div class="loader"></div>';
            
            // Simulate registration
            setTimeout(() => {
                registerBtn.innerHTML = 'Create Account';
                showMessage(registerMessage, `Account created successfully! ${enable2FA ? '2FA enabled.' : ''} ${enableBiometric ? 'Biometric authentication enabled.' : ''}`, 'success');
                
                // Clear form
                document.getElementById('register-username').value = '';
                document.getElementById('register-email').value = '';
                document.getElementById('register-password').value = '';
                document.getElementById('confirm-password').value = '';
            }, 2000);
        });
        
        // Helper functions
        function resetLoginSteps() {
            loginStep1.classList.add('active');
            loginStep2.classList.remove('active');
            loginSuccess.classList.remove('active');
            
            // Clear inputs
            document.getElementById('login-username').value = '';
            document.getElementById('login-password').value = '';
            otpInputs.forEach(input => {
                input.value = '';
            });
            
            // Clear messages
            loginMessage.classList.remove('success', 'error', 'info');
            loginMessage.style.display = 'none';
        }
        
        function showMessage(element, message, type) {
            element.textContent = message;
            element.className = 'status-message ' + type;
            element.style.display = 'block';
            
            // Auto-hide info messages after 5 seconds
            if (type === 'info') {
                setTimeout(() => {
                    element.style.display = 'none';
                }, 5000);
            }
        }
        
        function generateOTP() {
            // Generate a 6-digit random OTP
            return Math.floor(100000 + Math.random() * 900000).toString();
        }
        
        function simulateBiometricAuth(type) {
            const authType = type === 'fingerprint' ? 'Fingerprint' : 'Face ID';
            showMessage(loginMessage, `Scan your ${authType}...`, 'info');
            
            // Simulate biometric scanning
            setTimeout(() => {
                showMessage(loginMessage, `${authType} recognized!`, 'success');
                
                // Move to success step
                setTimeout(() => {
                    loginStep2.classList.remove('active');
                    loginSuccess.classList.add('active');
                }, 1000);
            }, 2000);
        }
        
        // Initialize the page
        document.addEventListener('DOMContentLoaded', () => {
            // For demo purposes, pre-fill login form
            document.getElementById('login-username').value = 'demo_user';
            document.getElementById('login-password').value = 'demo_password';
            
            // Show initial message
            showMessage(loginMessage, 'Demo credentials pre-filled. You can change them for testing.', 'info');
        });
    </script>
</body>
</html>
