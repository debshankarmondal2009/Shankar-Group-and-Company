import React, { useState, useEffect } from 'react';
import { 
  Layout, LogOut, Mail, Phone, User, Users, Microchip, 
  Send, Loader, Globe, Smartphone, Cpu, ShieldCheck, 
  ChevronRight, Facebook, MessageCircle, Edit3, Grid, 
  Briefcase, ShoppingCart, Database, Wifi, Lock
} from 'lucide-react';

// --- CONFIGURATION ---
const GOOGLE_SCRIPT_URL = "https://script.google.com/macros/s/AKfycbwJ2p53oRmKEMqWwZ97JTU942XaWx__nwf_q3aIddAoYB1KN6zhUhNRYKjwcQc7PF_Sew/exec";
const ADMIN_EMAIL = "debshankarmondal2009@gmail.com";
const ADMIN_PHONE = "8927256859";
const ADMIN_PASS = "dangermr48@gmail.com";
const WHATSAPP_LINK = "https://wa.me/message/25IAURX3TBULA1";

// --- SERVICES DATA (10 Verticals) ---
const INITIAL_SERVICES = [
  { id: 1, name: 'Semiconductor Design', icon: Microchip, desc: 'Advanced chip architecture & lithography.' },
  { id: 2, name: 'Cloud Infrastructure', icon: Globe, desc: 'Scalable AWS/Azure server ecosystems.' },
  { id: 3, name: 'AI & Machine Learning', icon: Cpu, desc: 'Neural networks & automation bots.' },
  { id: 4, name: 'Cyber Security', icon: ShieldCheck, desc: 'Enterprise-grade firewall & data defense.' },
  { id: 5, name: 'Blockchain Solutions', icon: Lock, desc: 'Secure Web3 & crypto-ledger systems.' },
  { id: 6, name: 'Mobile App Ecosystem', icon: Smartphone, desc: 'iOS & Android cross-platform dev.' },
  { id: 7, name: 'E-Commerce Tech', icon: ShoppingCart, desc: 'Global trade & payment gateways.' },
  { id: 8, name: 'IoT Systems', icon: Wifi, desc: 'Smart home & industrial automation.' },
  { id: 9, name: 'Big Data Analytics', icon: Database, desc: 'Business intelligence & processing.' },
  { id: 10, name: 'FinTech', icon: Layout, desc: 'Next-gen financial technology.' }
];

// --- API HELPER ---
const apiCall = async (payload) => {
  try {
    await fetch(GOOGLE_SCRIPT_URL, {
      method: "POST",
      mode: "no-cors",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(payload),
    });
    return true;
  } catch (error) {
    console.error("API Error:", error);
    return false;
  }
};

export default function App() {
  const [view, setView] = useState('splash'); // splash, auth, dashboard
  const [user, setUser] = useState(null); // { name, role: 'Admin' | 'User' }
  const [services, setServices] = useState(INITIAL_SERVICES);
  const [loading, setLoading] = useState(false);

  // Splash Screen Timer
  useEffect(() => {
    if (view === 'splash') {
      setTimeout(() => setView('auth'), 2500);
    }
  }, [view]);

  // Handle Login
  const handleLogin = (data) => {
    setLoading(true);
    setTimeout(() => {
      let role = 'User';
      // Admin Check Logic
      if ((data.email === ADMIN_EMAIL || data.phone === ADMIN_PHONE) && data.password === ADMIN_PASS) {
        role = 'Admin';
      }
      
      const userData = { ...data, role };
      setUser(userData);
      
      // Save to Google Sheet
      apiCall({ action: 'login', ...userData });
      
      setLoading(false);
      setView('dashboard');
    }, 1500);
  };

  // Handle Job Application
  const handleJobSubmit = (jobData) => {
    setLoading(true);
    // 1. Save to Sheet
    apiCall({ action: 'apply', ...jobData, name: user?.name, phone: user?.phone });

    // 2. WhatsApp Redirect
    const text = `Hello Shankar Group, I am applying for a job.%0A%0AName: ${user?.name}%0AQual: ${jobData.qual}%0ASector: ${jobData.sector}%0AExp: ${jobData.exp}%0APhone: ${user?.phone}`;
    window.open(`${WHATSAPP_LINK}?text=${text}`, '_blank');
    
    setLoading(false);
    alert("Application Submitted! Redirecting to WhatsApp...");
  };

  if (view === 'splash') return <SplashScreen />;
  if (view === 'auth') return <AuthScreen onLogin={handleLogin} />;
  
  return (
    <div className="min-h-screen bg-[#0B0D17] text-white font-sans selection:bg-[#00CFFF] selection:text-black">
      {/* Header */}
      <nav className="fixed top-0 w-full bg-[#0B0D17]/90 backdrop-blur-md border-b border-white/10 z-50 px-6 h-16 flex items-center justify-between">
        <div className="flex items-center gap-2">
          <Microchip className="text-[#00CFFF]" /> 
          <span className="font-bold tracking-tight">SHANKAR GROUP</span>
        </div>
        <div className="flex items-center gap-3">
           {user?.role === 'Admin' && <span className="bg-red-500/20 text-red-400 text-xs px-2 py-1 rounded border border-red-500/50">CEO MODE</span>}
           <button onClick={() => setView('auth')} className="p-2 bg-white/5 rounded-full hover:bg-white/10"><LogOut size={18}/></button>
        </div>
      </nav>

      {/* Main Content */}
      <main className="pt-20 pb-24 px-4 max-w-4xl mx-auto space-y-12">
        {/* Hero Section */}
        <section className="text-center space-y-4 py-10">
          <h1 className="text-4xl md:text-6xl font-black bg-clip-text text-transparent bg-gradient-to-r from-[#00CFFF] to-[#A06FFF]">
            {user?.role === 'Admin' ? "CEO CONTROL PANEL" : "BUILDING THE FUTURE"}
          </h1>
          <p className="text-gray-400">Welcome back, <span className="text-white font-bold">{user?.name}</span></p>
        </section>

        {/* Services Grid */}
        <section>
          <h2 className="text-2xl font-bold mb-6 flex items-center gap-2"><Grid className="text-[#00CFFF]"/> Our Services</h2>
          <div className="grid grid-cols-2 md:grid-cols-2 gap-4">
            {services.map(s => (
              <div key={s.id} className="bg-[#151725] p-5 rounded-2xl border border-white/5 hover:border-[#00CFFF]/50 transition-all group relative">
                {user?.role === 'Admin' && <Edit3 size={16} className="absolute top-3 right-3 text-red-400 cursor-pointer"/>}
                <s.icon className="text-[#00CFFF] mb-3 group-hover:scale-110 transition-transform" size={32} />
                <h3 className="font-bold">{s.name}</h3>
                <p className="text-xs text-gray-500 mt-1">{s.desc}</p>
              </div>
            ))}
          </div>
        </section>

        {/* Career Section */}
        <section className="bg-[#151725] p-6 rounded-3xl border border-white/5">
          <h2 className="text-2xl font-bold mb-6 flex items-center gap-2"><Briefcase className="text-[#A06FFF]"/> Join Our Team</h2>
          <form onSubmit={(e) => {
            e.preventDefault();
            handleJobSubmit({
              qual: e.target.qual.value,
              sector: e.target.sector.value,
              exp: e.target.exp.value
            });
          }} className="space-y-4">
            <input name="qual" placeholder="Qualification" required className="w-full bg-[#0B0D17] p-4 rounded-xl border border-white/10 outline-none focus:border-[#00CFFF]" />
            <select name="sector" className="w-full bg-[#0B0D17] p-4 rounded-xl border border-white/10 outline-none focus:border-[#00CFFF] text-gray-300">
              {services.map(s => <option key={s.id} value={s.name}>{s.name}</option>)}
            </select>
            <input name="exp" placeholder="Experience (Years)" required className="w-full bg-[#0B0D17] p-4 rounded-xl border border-white/10 outline-none focus:border-[#00CFFF]" />
            <button disabled={loading} className="w-full bg-gradient-to-r from-[#00CFFF] to-[#A06FFF] p-4 rounded-xl font-bold text-white hover:opacity-90">
              {loading ? "Processing..." : "Submit & Send on WhatsApp"}
            </button>
          </form>
        </section>

        {/* Contact Footer */}
        <section className="text-center space-y-4 pt-8 border-t border-white/5">
          <div className="flex justify-center gap-6">
            <a href="https://www.facebook.com/share/18b7qxXR7m/" target="_blank" className="p-3 bg-[#151725] rounded-full text-blue-500"><Facebook /></a>
            <a href={WHATSAPP_LINK} target="_blank" className="p-3 bg-[#151725] rounded-full text-green-500"><MessageCircle /></a>
          </div>
          <p className="text-gray-600 text-xs">© 2026 Shankar Group & Company Ltd.</p>
        </section>
      </main>
    </div>
  );
}

// --- SUB COMPONENTS ---

const SplashScreen = () => (
  <div className="fixed inset-0 bg-[#0B0D17] flex flex-col items-center justify-center z-50">
    <Microchip size={64} className="text-[#00CFFF] animate-pulse" />
    <h1 className="text-3xl font-black text-white mt-4 tracking-tighter">SHANKAR GROUP</h1>
    <div className="w-32 h-1 bg-gray-800 rounded-full mt-6 overflow-hidden">
      <div className="h-full bg-[#00CFFF] w-full animate-[ping_1s_ease-in-out_infinite]"></div>
    </div>
  </div>
);

const AuthScreen = ({ onLogin }) => {
  const [data, setData] = useState({ name: '', email: '', phone: '', password: '' });
  
  return (
    <div className="min-h-screen bg-[#0B0D17] flex items-center justify-center p-4">
      <div className="w-full max-w-md bg-[#151725] p-8 rounded-3xl border border-white/10">
        <h2 className="text-2xl font-bold text-white mb-2 text-center">Portal Login</h2>
        <p className="text-gray-500 text-sm text-center mb-6">Access the Enterprise Dashboard</p>
        <form onSubmit={(e) => { e.preventDefault(); onLogin(data); }} className="space-y-4">
          <input placeholder="Full Name" required onChange={e=>setData({...data, name:e.target.value})} className="w-full bg-[#0B0D17] p-4 rounded-xl border border-white/10 text-white outline-none focus:border-[#00CFFF]" />
          <input placeholder="Email" type="email" onChange={e=>setData({...data, email:e.target.value})} className="w-full bg-[#0B0D17] p-4 rounded-xl border border-white/10 text-white outline-none focus:border-[#00CFFF]" />
          <input placeholder="Phone" onChange={e=>setData({...data, phone:e.target.value})} className="w-full bg-[#0B0D17] p-4 rounded-xl border border-white/10 text-white outline-none focus:border-[#00CFFF]" />
          <input placeholder="Password" type="password" required onChange={e=>setData({...data, password:e.target.value})} className="w-full bg-[#0B0D17] p-4 rounded-xl border border-white/10 text-white outline-none focus:border-[#00CFFF]" />
          <button className="w-full bg-[#00CFFF] text-black font-bold p-4 rounded-xl hover:bg-[#00CFFF]/90 transition-colors">Enter System</button>
        </form>
      </div>
    </div>
  );
};
