# cashphone
cashphone
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";
import { BrowserRouter, Routes, Route } from "react-router-dom";
import { Toaster } from "@/components/ui/toaster";
import { Toaster as Sonner } from "@/components/ui/sonner";
import { TooltipProvider } from "@/components/ui/tooltip";
import { LanguageProvider } from "@/contexts/LanguageContext";
import Welcome from "@/components/Welcome";
import Register from "@/pages/Register";
import Login from "@/pages/Login";
import Dashboard from "@/pages/Dashboard";

const queryClient = new QueryClient();

const App = () => (
  <QueryClientProvider client={queryClient}>
    <LanguageProvider>
      <TooltipProvider>
        <Toaster />
        <Sonner />
        <BrowserRouter>
          <Routes>
            <Route path="/" element={<Welcome />} />
            <Route path="/register/:accountType" element={<Register />} />
            <Route path="/login" element={<Login />} />
            <Route path="/dashboard" element={<Dashboard />} />
            {/* الصفحات الإضافية ستضاف لاحقًا */}
          </Routes>
        </BrowserRouter>
      </TooltipProvider>
    </LanguageProvider>
  </QueryClientProvider>
);

export default App;




import React from 'react';
import { Button } from '@/components/ui/button';
import { Card, CardContent } from '@/components/ui/card';
import { useLanguage } from '@/contexts/LanguageContext';
import { Link } from 'react-router-dom';

const Welcome = () => {
  const { t, language, setLanguage } = useLanguage();

  return (
    <div className={`min-h-screen flex flex-col items-center justify-center bg-gradient-to-br from-amber-900/90 to-amber-800 p-4 ${language === 'ar' ? 'font-arabic' : ''}`}>
      <div className="w-full max-w-md text-center mb-2">
        <div className="flex justify-center items-center mb-2">
          <img 
            src="/lovable-uploads/23f1afbb-d953-43ee-afdb-26bfe6cfb90f.png" 
            alt="Cash Phone Logo" 
            className="w-32 h-32 object-contain"
          />
        </div>
        <h1 className={`text-3xl font-bold text-amber-400 mb-2 ${language === 'ar' ? 'font-arabic' : ''}`}>
          {t('welcome')}
        </h1>
        
        <div className="flex justify-center gap-2 mb-6">
          <Button
            variant={language === 'ar' ? 'default' : 'outline'}
            onClick={() => setLanguage('ar')}
            className={language === 'ar' ? 'bg-amber-400 hover:bg-amber-500 text-amber-950' : 'text-amber-400 border-amber-400 hover:bg-amber-400/10'}
          >
            عربي
          </Button>
          <Button
            variant={language === 'en' ? 'default' : 'outline'}
            onClick={() => setLanguage('en')}
            className={language === 'en' ? 'bg-amber-400 hover:bg-amber-500 text-amber-950' : 'text-amber-400 border-amber-400 hover:bg-amber-400/10'}
          >
            English
          </Button>
        </div>
      </div>

      <Card className="w-full max-w-md bg-amber-950/80 border-amber-400/30 text-amber-50 backdrop-blur-md">
        <CardContent className="p-6 space-y-6">
          <div className="space-y-4">
            <Link to="/register/personal" className="block w-full">
              <Button
                className="w-full bg-amber-400 hover:bg-amber-500 text-amber-950"
              >
                {t('personalAccount')}
              </Button>
            </Link>
            <Link to="/register/business" className="block w-full">
              <Button
                className="w-full bg-transparent border border-amber-400 text-amber-400 hover:bg-amber-400/10"
              >
                {t('businessAccount')}
              </Button>
            </Link>
          </div>

          <div className="pt-4 text-center border-t border-amber-400/20">
            <p className="text-sm text-amber-200">
              {language === 'ar' ? 'لديك حساب بالفعل؟' : 'Already have an account?'}
            </p>
            <Link to="/login" className="block">
              <Button 
                variant="link" 
                className="mt-1 text-amber-400 hover:text-amber-300"
              >
                {t('login')}
              </Button>
            </Link>
          </div>
        </CardContent>
      </Card>
    </div>
  );
};

export default Welcome;





import React, { createContext, useContext, useState } from 'react';

type Language = 'ar' | 'en';

interface LanguageContextType {
  language: Language;
  setLanguage: (lang: Language) => void;
  t: (key: string) => string;
}

const translations = {
  ar: {
    welcome: 'مرحباً بك في كاش فون',
    personalAccount: 'حساب شخصي',
    businessAccount: 'حساب تجاري',
    governmentAccount: 'حساب حكومي',
    register: 'تسجيل',
    login: 'تسجيل الدخول',
    name: 'الاسم',
    phone: 'رقم الهاتف',
    gender: 'الجنس',
    male: 'ذكر',
    female: 'أنثى',
    uploadPhoto: 'رفع صورة شخصية',
    uploadID: 'رفع صورة الهوية',
    continue: 'متابعة',
    password: 'كلمة المرور',
    confirmPassword: 'تأكيد كلمة المرور',
    back: 'رجوع',
    next: 'التالي',
    finish: 'إنهاء',
    passwordRequirements: 'كلمة المرور يجب أن تحتوي على 8 أحرف على الأقل',
    // الترجمات الجديدة للوحة التحكم
    accountBalance: 'رصيد الحساب',
    services: 'الخدمات',
    bills: 'فواتير',
    telecom: 'اتصالات',
    transfers: 'تحويلات',
    shopping: 'تسوق',
    settings: 'الإعدادات',
    digitalCard: 'البطاقة الرقمية',
    recentTransactions: 'العمليات الأخيرة',
    cardholderName: 'اسم العميل',
    expiryDate: 'تاريخ الإنتهاء',
    cvv: 'الرمز',
  },
  en: {
    welcome: 'Welcome to Cash Phone',
    personalAccount: 'Personal Account',
    businessAccount: 'Business Account',
    governmentAccount: 'Government Account',
    register: 'Register',
    login: 'Login',
    name: 'Name',
    phone: 'Phone Number',
    gender: 'Gender',
    male: 'Male',
    female: 'Female',
    uploadPhoto: 'Upload Photo',
    uploadID: 'Upload ID',
    continue: 'Continue',
    password: 'Password',
    confirmPassword: 'Confirm Password',
    back: 'Back',
    next: 'Next',
    finish: 'Finish',
    passwordRequirements: 'Password must be at least 8 characters long',
    // New translations for dashboard
    accountBalance: 'Account Balance',
    services: 'Services',
    bills: 'Bills',
    telecom: 'Telecom',
    transfers: 'Transfers',
    shopping: 'Shopping',
    settings: 'Settings',
    digitalCard: 'Digital Card',
    recentTransactions: 'Recent Transactions',
    cardholderName: 'Cardholder Name',
    expiryDate: 'Expiry Date',
    cvv: 'CVV',
  },
};

const LanguageContext = createContext<LanguageContextType | undefined>(undefined);

export const LanguageProvider: React.FC<{ children: React.ReactNode }> = ({ children }) => {
  const [language, setLanguage] = useState<Language>('ar');

  const t = (key: string): string => {
    return translations[language][key as keyof typeof translations['en']] || key;
  };

  return (
    <LanguageContext.Provider value={{ language, setLanguage, t }}>
      {children}
    </LanguageContext.Provider>
  );
};

export const useLanguage = () => {
  const context = useContext(LanguageContext);
  if (!context) {
    throw new Error('useLanguage must be used within a LanguageProvider');
  }
  return context;
};

import React, { useState } from 'react';
import { useNavigate } from 'react-router-dom';
import { useLanguage } from '@/contexts/LanguageContext';
import { Card, CardContent } from '@/components/ui/card';
import { Button } from '@/components/ui/button';
import { 
  CreditCard, 
  Phone, 
  ArrowRight, 
  ArrowLeft, 
  Settings, 
  ShoppingCart,
  Home
} from 'lucide-react';

const Dashboard = () => {
  const { t, language } = useLanguage();
  const navigate = useNavigate();
  
  // Mock data for account balance
  const [balances] = useState({
    yer: 150000,
    sar: 2500,
    usd: 500
  });

  const services = [
    { name: language === 'ar' ? 'فواتير' : 'Bills', icon: <Home className="h-6 w-6" />, route: '/bills' },
    { name: language === 'ar' ? 'اتصالات' : 'Telecom', icon: <Phone className="h-6 w-6" />, route: '/telecom' },
    { name: language === 'ar' ? 'تحويلات' : 'Transfers', icon: <ArrowRight className="h-6 w-6" />, route: '/transfers' },
    { name: language === 'ar' ? 'تسوق' : 'Shopping', icon: <ShoppingCart className="h-6 w-6" />, route: '/shopping' }
  ];

  const handleServiceClick = (route: string) => {
    navigate(route);
  };

  const formatCurrency = (amount: number, currency: string) => {
    switch (currency) {
      case 'yer':
        return `${amount.toLocaleString()} ${language === 'ar' ? 'ريال يمني' : 'YER'}`;
      case 'sar':
        return `${amount.toLocaleString()} ${language === 'ar' ? 'ريال سعودي' : 'SAR'}`;
      case 'usd':
        return `${amount.toLocaleString()} ${language === 'ar' ? 'دولار' : 'USD'}`;
      default:
        return `${amount}`;
    }
  };

  return (
    <div className={`min-h-screen bg-gradient-to-br from-amber-900/90 to-amber-800 p-4 ${language === 'ar' ? 'font-arabic' : ''}`}>
      <div className="max-w-md mx-auto">
        {/* Header */}
        <div className="flex justify-between items-center mb-6">
          <h1 className="text-2xl font-bold text-amber-400">
            {language === 'ar' ? 'كاش فون' : 'Cash Phone'}
          </h1>
          <Button
            variant="ghost"
            onClick={() => navigate('/settings')}
            className="text-amber-400 hover:text-amber-300"
          >
            <Settings className="h-6 w-6" />
          </Button>
        </div>

        {/* Balance Cards */}
        <div className="mb-6">
          <h2 className="text-xl font-medium text-amber-200 mb-3">
            {language === 'ar' ? 'رصيد الحساب' : 'Account Balance'}
          </h2>
          <div className="space-y-3">
            <Card className="bg-amber-950/80 border-amber-400/30 text-amber-50 overflow-hidden">
              <CardContent className="p-4">
                <div className="flex justify-between items-center">
                  <div>
                    <p className="text-amber-300 text-sm">
                      {language === 'ar' ? 'ريال يمني' : 'Yemeni Rial'}
                    </p>
                    <p className="text-2xl font-bold text-amber-50">
                      {formatCurrency(balances.yer, 'yer')}
                    </p>
                  </div>
                  <div className="h-10 w-10 bg-amber-400 rounded-full flex items-center justify-center">
                    <CreditCard className="h-5 w-5 text-amber-950" />
                  </div>
                </div>
              </CardContent>
            </Card>
            
            <Card className="bg-amber-950/80 border-amber-400/30 text-amber-50">
              <CardContent className="p-4">
                <div className="flex justify-between items-center">
                  <div>
                    <p className="text-amber-300 text-sm">
                      {language === 'ar' ? 'ريال سعودي' : 'Saudi Riyal'}
                    </p>
                    <p className="text-2xl font-bold text-amber-50">
                      {formatCurrency(balances.sar, 'sar')}
                    </p>
                  </div>
                  <div className="h-10 w-10 bg-amber-400 rounded-full flex items-center justify-center">
                    <CreditCard className="h-5 w-5 text-amber-950" />
                  </div>
                </div>
              </CardContent>
            </Card>
            
            <Card className="bg-amber-950/80 border-amber-400/30 text-amber-50">
              <CardContent className="p-4">
                <div className="flex justify-between items-center">
                  <div>
                    <p className="text-amber-300 text-sm">
                      {language === 'ar' ? 'دولار أمريكي' : 'US Dollar'}
                    </p>
                    <p className="text-2xl font-bold text-amber-50">
                      {formatCurrency(balances.usd, 'usd')}
                    </p>
                  </div>
                  <div className="h-10 w-10 bg-amber-400 rounded-full flex items-center justify-center">
                    <CreditCard className="h-5 w-5 text-amber-950" />
                  </div>
                </div>
              </CardContent>
            </Card>
          </div>
        </div>

        {/* Services */}
        <div className="mb-6">
          <h2 className="text-xl font-medium text-amber-200 mb-3">
            {language === 'ar' ? 'الخدمات' : 'Services'}
          </h2>
          <div className="grid grid-cols-2 gap-3">
            {services.map((service, index) => (
              <Card 
                key={index}
                className="bg-amber-950/80 border-amber-400/30 text-amber-50 hover:bg-amber-900/90 transition-colors cursor-pointer"
                onClick={() => handleServiceClick(service.route)}
              >
                <CardContent className="p-4 flex flex-col items-center justify-center text-center">
                  <div className="h-12 w-12 bg-amber-400/20 rounded-full flex items-center justify-center mb-2">
                    {service.icon}
                  </div>
                  <p className="text-amber-200">{service.name}</p>
                </CardContent>
              </Card>
            ))}
          </div>
        </div>

        {/* Digital Card */}
        <div className="mb-6">
          <h2 className="text-xl font-medium text-amber-200 mb-3">
            {language === 'ar' ? 'البطاقة الرقمية' : 'Digital Card'}
          </h2>
          <Card 
            className="bg-gradient-to-r from-amber-700 to-amber-600 border-amber-400/50 text-amber-50"
            onClick={() => navigate('/digital-card')}
          >
            <CardContent className="p-4 relative overflow-hidden">
              <div className="absolute top-0 right-0 left-0 h-12 bg-gradient-to-r from-amber-500/20 to-amber-300/20" />
              <div className="relative z-10">
                <div className="flex justify-between items-center mb-6">
                  <img 
                    src="/lovable-uploads/23f1afbb-d953-43ee-afdb-26bfe6cfb90f.png" 
                    alt="Cash Phone Logo" 
                    className="w-12 h-12 object-contain"
                  />
                  <p className="text-amber-200 font-bold">
                    {language === 'ar' ? 'كاش فون' : 'CASH PHONE'}
                  </p>
                </div>
                <p className="text-amber-100 mb-1 text-sm">
                  {language === 'ar' ? 'اسم العميل' : 'Cardholder Name'}
                </p>
                <p className="text-amber-50 font-bold mb-4 truncate">
                  محمد علي الحميدي
                </p>
                <div className="flex justify-between items-center">
                  <div>
                    <p className="text-amber-100 mb-1 text-xs">
                      {language === 'ar' ? 'تاريخ الإنتهاء' : 'Expiry Date'}
                    </p>
                    <p className="text-amber-50 font-bold">04/28</p>
                  </div>
                  <div>
                    <p className="text-amber-100 mb-1 text-xs">
                      {language === 'ar' ? 'الرمز' : 'CVV'}
                    </p>
                    <p className="text-amber-50 font-bold">***</p>
                  </div>
                </div>
              </div>
            </CardContent>
          </Card>
        </div>

        {/* Recent Transactions Button */}
        <Button
          className="w-full bg-amber-400 hover:bg-amber-500 text-amber-950 flex items-center justify-between"
          onClick={() => navigate('/transactions')}
        >
          {language === 'ar' ? 'العمليات الأخيرة' : 'Recent Transactions'}
          {language === 'ar' ? (
            <ArrowLeft className="h-4 w-4 ml-2" />
          ) : (
            <ArrowRight className="h-4 w-4 ml-2" />
          )}
        </Button>
      </div>
    </div>
  );
};

export default Dashboard;

import React, { useState } from 'react';
import { useNavigate } from 'react-router-dom';
import { useLanguage } from '@/contexts/LanguageContext';
import { Card, CardContent } from '@/components/ui/card';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { Label } from '@/components/ui/label';
import { Fingerprint, User, Lock } from 'lucide-react';

const Login = () => {
  const { t, language } = useLanguage();
  const navigate = useNavigate();
  const [loginMethod, setLoginMethod] = useState<'password' | 'fingerprint' | 'face'>('password');
  const [phone, setPhone] = useState('');
  const [password, setPassword] = useState('');

  const handleLogin = (e: React.FormEvent) => {
    e.preventDefault();
    console.log('Login attempt with:', { phone, password, method: loginMethod });
    // لأغراض العرض التوضيحي، سننتقل مباشرة إلى صفحة لوحة التحكم
    navigate('/dashboard');
  };

  return (
    <div className={`min-h-screen flex flex-col items-center justify-center bg-gradient-to-br from-amber-900/90 to-amber-800 p-4 ${language === 'ar' ? 'font-arabic' : ''}`}>
      <Card className="w-full max-w-md bg-amber-950/80 border-amber-400/30 text-amber-50 backdrop-blur-md">
        <CardContent className="p-6">
          <h2 className="text-2xl font-bold text-amber-400 text-center mb-6">
            {t('login')}
          </h2>

          <form onSubmit={handleLogin} className="space-y-4">
            <div className="space-y-2">
              <Label htmlFor="phone">{t('phone')}</Label>
              <Input
                id="phone"
                type="tel"
                value={phone}
                onChange={(e) => setPhone(e.target.value)}
                className="bg-amber-950/30 border-amber-400/30 text-amber-50"
                required
              />
            </div>

            <div className="flex justify-center space-x-4 my-6">
              <Button
                type="button"
                variant={loginMethod === 'password' ? 'default' : 'outline'}
                className={
                  loginMethod === 'password'
                    ? 'bg-amber-400 text-amber-950 hover:bg-amber-500'
                    : 'border-amber-400 text-amber-400 hover:bg-amber-400/10'
                }
                onClick={() => setLoginMethod('password')}
              >
                <Lock className="h-4 w-4 mr-2" />
                {language === 'ar' ? 'كلمة المرور' : 'Password'}
              </Button>
              <Button
                type="button"
                variant={loginMethod === 'fingerprint' ? 'default' : 'outline'}
                className={
                  loginMethod === 'fingerprint'
                    ? 'bg-amber-400 text-amber-950 hover:bg-amber-500'
                    : 'border-amber-400 text-amber-400 hover:bg-amber-400/10'
                }
                onClick={() => setLoginMethod('fingerprint')}
              >
                <Fingerprint className="h-4 w-4 mr-2" />
                {language === 'ar' ? 'بصمة' : 'Fingerprint'}
              </Button>
              <Button
                type="button"
                variant={loginMethod === 'face' ? 'default' : 'outline'}
                className={
                  loginMethod === 'face'
                    ? 'bg-amber-400 text-amber-950 hover:bg-amber-500'
                    : 'border-amber-400 text-amber-400 hover:bg-amber-400/10'
                }
                onClick={() => setLoginMethod('face')}
              >
                <User className="h-4 w-4 mr-2" />
                {language === 'ar' ? 'بصمة وجه' : 'Face ID'}
              </Button>
            </div>

            {loginMethod === 'password' && (
              <div className="space-y-2">
                <Label htmlFor="password">{t('password')}</Label>
                <Input
                  id="password"
                  type="password"
                  value={password}
                  onChange={(e) => setPassword(e.target.value)}
                  className="bg-amber-950/30 border-amber-400/30 text-amber-50"
                  required
                />
              </div>
            )}

            {loginMethod !== 'password' && (
              <div className="flex justify-center py-6">
                {loginMethod === 'fingerprint' ? (
                  <Fingerprint className="h-24 w-24 text-amber-400" />
                ) : (
                  <User className="h-24 w-24 text-amber-400" />
                )}
              </div>
            )}

            <Button
              type="submit"
              className="w-full bg-amber-400 hover:bg-amber-500 text-amber-950 mt-6"
            >
              {t('login')}
            </Button>

            <div className="text-center mt-4">
              <Button
                type="button"
                variant="link"
                onClick={() => navigate('/')}
                className="text-amber-400 hover:text-amber-300"
              >
                {language === 'ar' ? 'العودة إلى الصفحة الرئيسية' : 'Back to home'}
              </Button>
            </div>
          </form>
        </CardContent>
      </Card>
    </div>
  );
};

export default Login;
![24B54519-19E4-423F-9C98-4676921E70FD](https://github.com/user-attachments/as
sets/742c0f32-bde4-435a-a6a3-1e5489ca136c)

