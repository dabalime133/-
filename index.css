import { useState, useEffect, useRef } from "react";

const CASINO_LINK = "https://lkiv.cc/dea2";
const LOGO_URL =
  "https://raw.githubusercontent.com/dabalime133/aviator/main/public/images/aviator-plane.png";

/* ─── Floating particles background ─────────────────────────── */
function Particles() {
  return (
    <div className="pointer-events-none absolute inset-0 overflow-hidden">
      {Array.from({ length: 30 }).map((_, i) => (
        <span
          key={i}
          className="absolute rounded-full opacity-20"
          style={{
            width: `${Math.random() * 6 + 2}px`,
            height: `${Math.random() * 6 + 2}px`,
            background: i % 3 === 0 ? "#ff4d4d" : i % 3 === 1 ? "#ff9900" : "#ffffff",
            left: `${Math.random() * 100}%`,
            top: `${Math.random() * 100}%`,
            animation: `floatUp ${Math.random() * 6 + 4}s linear ${Math.random() * 5}s infinite`,
          }}
        />
      ))}
    </div>
  );
}

/* ─── Animated multiplier counter ────────────────────────────── */
function MultiplierCounter() {
  const [value, setvalue] = useState(1.0);
  const [crashed, setCrashed] = useState(false);
  const [phase, setPhase] = useState<"waiting" | "flying" | "crashed">("waiting");
  const timer = useRef<ReturnType<typeof setInterval> | null>(null);

  useEffect(() => {
    let v = 1.0;
    let crashPoint = Math.random() * 8 + 1.5;
    let step = 0;

    const start = () => {
      setPhase("waiting");
      setCrashed(false);
      setvalue(1.0);
      v = 1.0;
      crashPoint = Math.random() * 10 + 1.5;
      step = 0;

      setTimeout(() => {
        setPhase("flying");
        timer.current = setInterval(() => {
          step++;
          const growth = 1 + step * 0.008 + Math.pow(step * 0.003, 1.5);
          v = Math.round(growth * 100) / 100;
          setvalue(v);
          if (v >= crashPoint) {
            clearInterval(timer.current!);
            setCrashed(true);
            setPhase("crashed");
            setTimeout(start, 2500);
          }
        }, 80);
      }, 2000);
    };

    start();
    return () => {
      if (timer.current) clearInterval(timer.current);
    };
  }, []);

  const color =
    phase === "crashed"
      ? "text-red-500"
      : value < 2
      ? "text-green-400"
      : value < 5
      ? "text-yellow-400"
      : "text-orange-400";

  return (
    <div className="flex flex-col items-center gap-3">
      {phase === "waiting" && (
        <div className="text-gray-400 text-lg font-semibold animate-pulse tracking-widest font-mono">
          ОЖИДАНИЕ...
        </div>
      )}
      {phase !== "waiting" && (
        <>
          <div
            className={`font-black tabular-nums transition-colors duration-300 ${color}`}
            style={{
              fontFamily: "'Orbitron', monospace",
              fontSize: "clamp(3rem, 10vw, 6rem)",
              textShadow: crashed
                ? "0 0 30px rgba(255,50,50,0.8)"
                : "0 0 30px rgba(255,200,0,0.6)",
              letterSpacing: "-0.02em",
            }}
          >
            {crashed ? "CRASH!" : `${value.toFixed(2)}x`}
          </div>
          {!crashed && (
            <div className="flex gap-1">
              {[...Array(5)].map((_, i) => (
                <div
                  key={i}
                  className="w-1.5 h-1.5 rounded-full bg-yellow-400 animate-bounce"
                  style={{ animationDelay: `${i * 0.1}s` }}
                />
              ))}
            </div>
          )}
        </>
      )}
    </div>
  );
}

/* ─── Stats bar ──────────────────────────────────────────────── */
function StatBar({
  label,
  value,
  color,
}: {
  label: string;
  value: string;
  color: string;
}) {
  return (
    <div className="flex flex-col items-center gap-1">
      <div
        className={`text-2xl md:text-3xl font-black ${color}`}
        style={{ fontFamily: "'Orbitron', monospace" }}
      >
        {value}
      </div>
      <div className="text-xs text-gray-400 uppercase tracking-wider font-semibold">
        {label}
      </div>
    </div>
  );
}

/* ─── Strategy card ─────────────────────────────────────────── */
function StrategyCard({
  icon,
  title,
  risk,
  riskColor,
  desc,
  tips,
}: {
  icon: string;
  title: string;
  risk: string;
  riskColor: string;
  desc: string;
  tips: string[];
}) {
  return (
    <div className="relative group rounded-2xl overflow-hidden border border-white/10 bg-gradient-to-b from-white/5 to-transparent p-6 hover:border-red-500/40 transition-all duration-300 hover:shadow-[0_0_30px_rgba(255,77,77,0.15)]">
      <div className="absolute top-3 right-3">
        <span
          className={`text-xs font-bold px-3 py-1 rounded-full border ${riskColor}`}
        >
          {risk}
        </span>
      </div>
      <div className="text-4xl mb-3">{icon}</div>
      <h3 className="text-xl font-bold text-white mb-2">{title}</h3>
      <p className="text-gray-400 text-sm mb-4 leading-relaxed">{desc}</p>
      <ul className="space-y-1.5">
        {tips.map((tip, i) => (
          <li key={i} className="flex items-start gap-2 text-sm text-gray-300">
            <span className="text-red-400 mt-0.5 shrink-0">▸</span>
            {tip}
          </li>
        ))}
      </ul>
    </div>
  );
}

/* ─── Step card ─────────────────────────────────────────────── */
function StepCard({
  n,
  title,
  desc,
}: {
  n: number;
  title: string;
  desc: string;
}) {
  return (
    <div className="relative flex gap-4 items-start">
      <div className="relative shrink-0">
        <div
          className="w-12 h-12 rounded-full bg-gradient-to-br from-red-500 to-orange-500 flex items-center justify-center font-black text-white text-lg shadow-lg shadow-red-500/30"
          style={{ fontFamily: "'Orbitron', monospace" }}
        >
          {n}
        </div>
        {n < 5 && (
          <div className="absolute left-1/2 top-full w-0.5 h-8 bg-gradient-to-b from-red-500/40 to-transparent -translate-x-1/2 hidden md:block" />
        )}
      </div>
      <div className="pt-2">
        <h3 className="font-bold text-white text-lg mb-1">{title}</h3>
        <p className="text-gray-400 text-sm leading-relaxed">{desc}</p>
      </div>
    </div>
  );
}

/* ─── FAQ item ──────────────────────────────────────────────── */
function FaqItem({ q, a }: { q: string; a: string }) {
  const [open, setOpen] = useState(false);
  return (
    <div
      className={`rounded-xl border transition-all duration-300 cursor-pointer ${
        open
          ? "border-red-500/40 bg-red-500/5"
          : "border-white/10 bg-white/3 hover:border-white/20"
      }`}
      onClick={() => setOpen((p) => !p)}
    >
      <div className="flex justify-between items-center p-5 gap-4">
        <h4 className="font-semibold text-white text-sm md:text-base">{q}</h4>
        <span
          className={`text-xl shrink-0 transition-transform duration-300 ${
            open ? "rotate-45 text-red-400" : "text-gray-500"
          }`}
        >
          +
        </span>
      </div>
      {open && (
        <div className="px-5 pb-5 text-gray-400 text-sm leading-relaxed border-t border-white/5 pt-4">
          {a}
        </div>
      )}
    </div>
  );
}

/* ─── Live bets ticker ─────────────────────────────────────── */
const FAKE_BETS = [
  { name: "Alex***", bet: "500₽", multi: "2.40x", win: "1 200₽", color: "text-green-400" },
  { name: "Марк***", bet: "1 000₽", multi: "1.80x", win: "1 800₽", color: "text-green-400" },
  { name: "Kate***", bet: "200₽", multi: "5.10x", win: "1 020₽", color: "text-yellow-400" },
  { name: "Ivan***", bet: "750₽", multi: "CRASH", win: "-750₽", color: "text-red-400" },
  { name: "Ник***", bet: "300₽", multi: "12.50x", win: "3 750₽", color: "text-orange-400" },
  { name: "Oleg***", bet: "1 500₽", multi: "1.20x", win: "1 800₽", color: "text-green-400" },
  { name: "Юля***", bet: "100₽", multi: "CRASH", win: "-100₽", color: "text-red-400" },
  { name: "Дим***", bet: "2 000₽", multi: "3.30x", win: "6 600₽", color: "text-yellow-400" },
];

function LiveBets() {
  const [bets, setBets] = useState(FAKE_BETS);
  useEffect(() => {
    const iv = setInterval(() => {
      const names = ["Alex","Maxim","Kate","Nik","Dima","Oleg","Yulia","Ivan","Serg","Lena"];
      const multis = ["1.20x","1.50x","2.00x","3.10x","CRASH","5.40x","1.85x","CRASH","8.10x","1.30x"];
      const bets_list = [100,200,300,500,750,1000,1500,2000];
      const name = names[Math.floor(Math.random()*names.length)];
      const bet = bets_list[Math.floor(Math.random()*bets_list.length)];
      const multi = multis[Math.floor(Math.random()*multis.length)];
      const isCrash = multi === "CRASH";
      const multi_val = isCrash ? 0 : parseFloat(multi);
      const win = isCrash ? `-${bet}₽` : `${Math.round(bet * multi_val)} ₽`;
      const color = isCrash ? "text-red-400" : multi_val >= 5 ? "text-orange-400" : multi_val >= 2 ? "text-yellow-400" : "text-green-400";
      setBets(prev => [{name: `${name}***`, bet: `${bet}₽`, multi, win, color}, ...prev.slice(0, 7)]);
    }, 1800);
    return () => clearInterval(iv);
  }, []);

  return (
    <div className="overflow-hidden rounded-2xl border border-white/10 bg-black/30">
      <div className="flex items-center gap-3 px-5 py-3 bg-white/5 border-b border-white/10">
        <span className="relative flex h-2 w-2">
          <span className="animate-ping absolute inline-flex h-full w-full rounded-full bg-green-400 opacity-75"></span>
          <span className="relative inline-flex rounded-full h-2 w-2 bg-green-400"></span>
        </span>
        <span className="text-sm font-semibold text-white">СТАВКИ В РЕАЛЬНОМ ВРЕМЕНИ</span>
      </div>
      <div className="divide-y divide-white/5">
        {bets.map((b, i) => (
          <div
            key={i}
            className="flex items-center justify-between px-5 py-3 text-sm transition-all duration-300"
            style={{ animation: i === 0 ? "slideDown 0.4s ease" : undefined }}
          >
            <span className="text-gray-400 w-20 truncate">{b.name}</span>
            <span className="text-white font-semibold w-16 text-center">{b.bet}</span>
            <span className={`font-bold w-16 text-center ${b.color}`}>{b.multi}</span>
            <span className={`font-black w-20 text-right ${b.color}`}>{b.win}</span>
          </div>
        ))}
      </div>
    </div>
  );
}

/* ─── Testimonial ───────────────────────────────────────────── */
function Testimonial({
  name,
  text,
  stars,
  win,
}: {
  name: string;
  text: string;
  stars: number;
  win: string;
}) {
  return (
    <div className="rounded-2xl border border-white/10 bg-gradient-to-b from-white/5 to-transparent p-6 flex flex-col gap-4">
      <div className="flex items-start justify-between gap-3">
        <div>
          <div className="font-bold text-white">{name}</div>
          <div className="flex gap-0.5 mt-1">
            {Array.from({ length: stars }).map((_, i) => (
              <span key={i} className="text-yellow-400 text-sm">★</span>
            ))}
          </div>
        </div>
        <div className="text-right">
          <div className="text-xs text-gray-500 mb-1">Выигрыш</div>
          <div
            className="text-green-400 font-black text-lg"
            style={{ fontFamily: "'Orbitron', monospace" }}
          >
            {win}
          </div>
        </div>
      </div>
      <p className="text-gray-400 text-sm leading-relaxed italic">"{text}"</p>
    </div>
  );
}

/* ─── CTA Button ────────────────────────────────────────────── */
function CtaButton({
  children,
  size = "md",
  className = "",
}: {
  children: React.ReactNode;
  size?: "sm" | "md" | "lg";
  className?: string;
}) {
  const sizes = {
    sm: "px-6 py-3 text-sm",
    md: "px-8 py-4 text-base",
    lg: "px-10 py-5 text-lg",
  };
  return (
    <a
      href={CASINO_LINK}
      target="_blank"
      rel="noopener noreferrer"
      className={`relative inline-flex items-center justify-center gap-2 font-black rounded-xl text-white overflow-hidden group transition-all duration-300 hover:scale-105 active:scale-95 ${sizes[size]} ${className}`}
      style={{
        background: "linear-gradient(135deg, #ff4d4d 0%, #ff9900 100%)",
        boxShadow: "0 4px 30px rgba(255,77,77,0.4), inset 0 1px 0 rgba(255,255,255,0.2)",
      }}
    >
      <span className="absolute inset-0 bg-white/0 group-hover:bg-white/10 transition-all duration-300" />
      <span className="relative">{children}</span>
    </a>
  );
}

/* ─── MAIN APP ──────────────────────────────────────────────── */
export default function App() {
  const [scrolled, setScrolled] = useState(false);
  const [menuOpen, setMenuOpen] = useState(false);

  useEffect(() => {
    const onScroll = () => setScrolled(window.scrollY > 50);
    window.addEventListener("scroll", onScroll, { passive: true });
    return () => window.removeEventListener("scroll", onScroll);
  }, []);

  const scrollTo = (id: string) => {
    document.getElementById(id)?.scrollIntoView({ behavior: "smooth" });
    setMenuOpen(false);
  };

  return (
    <div
      className="min-h-screen text-white overflow-x-hidden"
      style={{
        background: "linear-gradient(180deg, #0a0a0f 0%, #12060f 50%, #0a0a0f 100%)",
        fontFamily: "'Montserrat', sans-serif",
      }}
    >
      {/* ── CSS Keyframes ── */}
      <style>{`
        @keyframes floatUp {
          0% { transform: translateY(0) scale(1); opacity: 0.15; }
          50% { opacity: 0.3; }
          100% { transform: translateY(-120vh) scale(0.5); opacity: 0; }
        }
        @keyframes slideDown {
          from { opacity: 0; transform: translateY(-16px); }
          to { opacity: 1; transform: translateY(0); }
        }
        @keyframes planeMove {
          0% { transform: translateX(-20px) translateY(0px) rotate(-5deg); }
          25% { transform: translateX(5px) translateY(-12px) rotate(3deg); }
          50% { transform: translateX(15px) translateY(-5px) rotate(-2deg); }
          75% { transform: translateX(5px) translateY(-18px) rotate(4deg); }
          100% { transform: translateX(-20px) translateY(0px) rotate(-5deg); }
        }
        @keyframes pulse-ring {
          0% { transform: scale(0.8); opacity: 1; }
          100% { transform: scale(1.8); opacity: 0; }
        }
        @keyframes shimmer {
          0% { background-position: -200% center; }
          100% { background-position: 200% center; }
        }
        @keyframes growLine {
          from { transform: scaleX(0); }
          to { transform: scaleX(1); }
        }
        @keyframes fadeInUp {
          from { opacity: 0; transform: translateY(30px); }
          to { opacity: 1; transform: translateY(0); }
        }
        .shimmer-text {
          background: linear-gradient(90deg, #ff4d4d, #ff9900, #fff, #ff9900, #ff4d4d);
          background-size: 200% auto;
          -webkit-background-clip: text;
          background-clip: text;
          -webkit-text-fill-color: transparent;
          animation: shimmer 4s linear infinite;
        }
        .glow-red { box-shadow: 0 0 40px rgba(255,77,77,0.3); }
        .grid-bg {
          background-image: linear-gradient(rgba(255,77,77,0.04) 1px, transparent 1px),
                            linear-gradient(90deg, rgba(255,77,77,0.04) 1px, transparent 1px);
          background-size: 40px 40px;
        }
        .number-card {
          background: linear-gradient(135deg, rgba(255,255,255,0.05) 0%, rgba(255,255,255,0.02) 100%);
        }
      `}</style>

      {/* ═══════════════════ NAVBAR ═══════════════════ */}
      <nav
        className={`fixed top-0 left-0 right-0 z-50 transition-all duration-300 ${
          scrolled
            ? "bg-black/80 backdrop-blur-md border-b border-white/10 py-3"
            : "bg-transparent py-4"
        }`}
      >
        <div className="max-w-7xl mx-auto px-4 flex items-center justify-between gap-4">
          {/* Logo */}
          <div className="flex items-center gap-3">
            <img
              src={LOGO_URL}
              alt="Aviator"
              className="h-9 w-auto object-contain"
              style={{ animation: "planeMove 6s ease-in-out infinite" }}
            />
            <span
              className="text-xl font-black text-white tracking-tight hidden sm:block"
              style={{ fontFamily: "'Orbitron', monospace" }}
            >
              AVIATOR
            </span>
          </div>

          {/* Desktop nav */}
          <div className="hidden md:flex items-center gap-6 text-sm font-semibold text-gray-300">
            {[["Как играть", "howto"], ["Стратегии", "strategies"], ["Отзывы", "reviews"], ["FAQ", "faq"]].map(
              ([label, id]) => (
                <button
                  key={id}
                  onClick={() => scrollTo(id)}
                  className="hover:text-white transition-colors"
                >
                  {label}
                </button>
              )
            )}
          </div>

          {/* CTA */}
          <div className="flex items-center gap-3">
            <CtaButton size="sm">
              🚀 Играть
            </CtaButton>
            <button
              className="md:hidden text-gray-300 hover:text-white p-1"
              onClick={() => setMenuOpen((p) => !p)}
            >
              <svg className="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                {menuOpen ? (
                  <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M6 18L18 6M6 6l12 12" />
                ) : (
                  <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M4 6h16M4 12h16M4 18h16" />
                )}
              </svg>
            </button>
          </div>
        </div>

        {/* Mobile menu */}
        {menuOpen && (
          <div className="md:hidden bg-black/95 border-t border-white/10 px-4 py-4 flex flex-col gap-3">
            {[["Как играть", "howto"], ["Стратегии", "strategies"], ["Отзывы", "reviews"], ["FAQ", "faq"]].map(
              ([label, id]) => (
                <button
                  key={id}
                  onClick={() => scrollTo(id)}
                  className="text-gray-300 hover:text-white font-semibold text-left py-2 border-b border-white/5 transition-colors"
                >
                  {label}
                </button>
              )
            )}
          </div>
        )}
      </nav>

      {/* ═══════════════════ HERO ═══════════════════ */}
      <section className="relative min-h-screen flex items-center justify-center pt-20 pb-10 grid-bg overflow-hidden">
        <Particles />

        {/* Decorative glows */}
        <div className="absolute top-1/3 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[600px] h-[600px] rounded-full pointer-events-none"
          style={{ background: "radial-gradient(circle, rgba(255,77,77,0.12) 0%, transparent 70%)" }} />
        <div className="absolute top-20 right-10 w-64 h-64 rounded-full pointer-events-none"
          style={{ background: "radial-gradient(circle, rgba(255,153,0,0.08) 0%, transparent 70%)" }} />

        <div className="relative max-w-5xl mx-auto px-4 text-center" style={{ animation: "fadeInUp 0.8s ease both" }}>
          {/* Badge */}
          <div className="inline-flex items-center gap-2 bg-red-500/10 border border-red-500/30 rounded-full px-4 py-2 text-sm text-red-400 font-semibold mb-8">
            <span className="relative flex h-2 w-2">
              <span className="animate-ping absolute inline-flex h-full w-full rounded-full bg-red-400 opacity-75"></span>
              <span className="relative inline-flex rounded-full h-2 w-2 bg-red-400"></span>
            </span>
            ИГРА ОНЛАЙН • RTP 97% • ПРОВАБЛИ ФЕА
          </div>

          {/* Plane + Multiplier */}
          <div className="flex justify-center mb-4">
            <img
              src={LOGO_URL}
              alt="Aviator plane"
              className="h-28 md:h-40 w-auto object-contain drop-shadow-[0_0_30px_rgba(255,150,0,0.5)]"
              style={{ animation: "planeMove 4s ease-in-out infinite" }}
            />
          </div>

          {/* Big multiplier display */}
          <div className="mb-6">
            <MultiplierCounter />
          </div>

          <h1
            className="font-black leading-none mb-4"
            style={{
              fontFamily: "'Orbitron', monospace",
              fontSize: "clamp(2.5rem, 8vw, 5rem)",
            }}
          >
            <span className="shimmer-text">AVIATOR</span>
            <br />
            <span className="text-white text-[0.55em] tracking-wider block mt-2">
              ВЗЛЕТИ К ПОБЕДЕ
            </span>
          </h1>

          <p className="text-gray-400 text-lg md:text-xl max-w-2xl mx-auto mb-10 leading-relaxed">
            Крупнейшая краш-игра в мире. Ставь — наблюдай — снимай выигрыш до того, как
            самолёт улетит. Каждая секунда на счету!
          </p>

          <div className="flex flex-col sm:flex-row gap-4 justify-center items-center mb-12">
            <CtaButton size="lg" className="w-full sm:w-auto">
              ✈️ ИГРАТЬ СЕЙЧАС — БЕСПЛАТНО
            </CtaButton>
            <button
              onClick={() => scrollTo("howto")}
              className="text-gray-400 hover:text-white font-semibold underline underline-offset-4 transition-colors text-sm"
            >
              Как это работает? →
            </button>
          </div>

          {/* Stats */}
          <div className="grid grid-cols-2 md:grid-cols-4 gap-6 max-w-2xl mx-auto">
            <StatBar label="Игроков онлайн" value="47K+" color="text-green-400" />
            <StatBar label="Выплачено" value="₽2.4M" color="text-yellow-400" />
            <StatBar label="Макс. множитель" value="100x" color="text-orange-400" />
            <StatBar label="RTP" value="97%" color="text-blue-400" />
          </div>
        </div>

        {/* Scroll indicator */}
        <div className="absolute bottom-8 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 text-gray-600 animate-bounce">
          <span className="text-xs tracking-widest uppercase">Скролл</span>
          <svg className="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M19 9l-7 7-7-7" />
          </svg>
        </div>
      </section>

      {/* ═══════════════════ LIVE BETS ═══════════════════ */}
      <section className="py-16 px-4">
        <div className="max-w-3xl mx-auto">
          <div className="text-center mb-8">
            <h2 className="text-2xl md:text-3xl font-black text-white mb-2">
              🔴 Прямой эфир ставок
            </h2>
            <p className="text-gray-500 text-sm">
              Тысячи игроков выигрывают прямо сейчас
            </p>
          </div>
          <LiveBets />
        </div>
      </section>

      {/* ═══════════════════ WHAT IS AVIATOR ═══════════════════ */}
      <section className="py-16 px-4 border-t border-white/5">
        <div className="max-w-6xl mx-auto">
          <div className="grid md:grid-cols-2 gap-12 items-center">
            <div>
              <div className="text-xs font-bold text-red-400 tracking-widest uppercase mb-3">
                О ИГРЕ
              </div>
              <h2
                className="text-3xl md:text-5xl font-black text-white mb-6 leading-tight"
                style={{ fontFamily: "'Orbitron', monospace" }}
              >
                ЧТО ТАКОЕ{" "}
                <span className="shimmer-text">AVIATOR?</span>
              </h2>
              <p className="text-gray-400 leading-relaxed mb-6">
                <strong className="text-white">Aviator</strong> — это революционная краш-игра от
                провайдера <strong className="text-red-400">Spribe</strong>, основанная на алгоритме
                Provably Fair. Самолёт взлетает, множитель растёт, и твоя задача — успеть нажать
                кнопку снятия до того, как самолёт улетит.
              </p>
              <p className="text-gray-400 leading-relaxed mb-8">
                Игра запущена в 2019 году и стала самой популярной crash-игрой в мире с аудиторией
                более <strong className="text-white">10 миллионов игроков</strong>. Каждый раунд —
                это уникальный криптографически случайный результат, который нельзя подделать.
              </p>
              <div className="grid grid-cols-3 gap-4">
                {[
                  { label: "Провайдер", value: "Spribe" },
                  { label: "Запущена", value: "2019" },
                  { label: "Игроков", value: "10M+" },
                ].map((s) => (
                  <div
                    key={s.label}
                    className="number-card rounded-xl p-4 text-center border border-white/10"
                  >
                    <div className="text-xl font-black text-white mb-1">{s.value}</div>
                    <div className="text-xs text-gray-500 uppercase tracking-wide">{s.label}</div>
                  </div>
                ))}
              </div>
            </div>

            <div className="relative">
              <div
                className="rounded-3xl overflow-hidden border border-white/10 p-8 text-center"
                style={{
                  background: "linear-gradient(135deg, rgba(255,77,77,0.1) 0%, rgba(255,153,0,0.05) 100%)",
                }}
              >
                <img
                  src={LOGO_URL}
                  alt="Aviator Game"
                  className="w-full max-w-xs mx-auto object-contain drop-shadow-[0_0_50px_rgba(255,150,0,0.4)]"
                  style={{ animation: "planeMove 5s ease-in-out infinite" }}
                />
                <div className="mt-6 space-y-3">
                  {[
                    "✅ Честная игра (Provably Fair)",
                    "✅ Мгновенные выплаты",
                    "✅ Ставки от 1₽",
                    "✅ Доступно 24/7",
                  ].map((f) => (
                    <div
                      key={f}
                      className="text-sm text-gray-300 font-semibold text-left"
                    >
                      {f}
                    </div>
                  ))}
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* ═══════════════════ HOW TO PLAY ═══════════════════ */}
      <section id="howto" className="py-20 px-4 grid-bg border-t border-white/5">
        <div className="max-w-5xl mx-auto">
          <div className="text-center mb-14">
            <div className="text-xs font-bold text-red-400 tracking-widest uppercase mb-3">
              ИНСТРУКЦИЯ
            </div>
            <h2
              className="text-3xl md:text-5xl font-black text-white mb-4"
              style={{ fontFamily: "'Orbitron', monospace" }}
            >
              КАК ИГРАТЬ?
            </h2>
            <p className="text-gray-500 max-w-xl mx-auto">
              Всего 5 простых шагов до первой победы
            </p>
          </div>

          <div className="grid md:grid-cols-2 gap-10 items-start">
            <div className="space-y-8">
              {[
                {
                  n: 1,
                  title: "Зарегистрируйся и пополни счёт",
                  desc: "Создай аккаунт в казино за 30 секунд. Внеси депозит любым удобным способом — от карты до криптовалюты.",
                },
                {
                  n: 2,
                  title: "Зайди в игру Aviator",
                  desc: "Найди игру в каталоге или используй поиск. Открой и выбери режим игры — демо или реальные деньги.",
                },
                {
                  n: 3,
                  title: "Сделай ставку до взлёта",
                  desc: "Перед каждым раундом есть окно для ставки (3–5 секунд). Можно делать одновременно ДВЕ ставки.",
                },
                {
                  n: 4,
                  title: "Наблюдай за множителем",
                  desc: "Самолёт взлетает и множитель растёт с 1.00x. Чем дольше ждёшь — тем больше потенциальный выигрыш.",
                },
                {
                  n: 5,
                  title: "Нажми «Снять» вовремя!",
                  desc: "Кликни кнопку ДО того, как самолёт улетит. Ставка × множитель = твой выигрыш. Автовывод доступен!",
                },
              ].map((s) => (
                <StepCard key={s.n} {...s} />
              ))}
            </div>

            <div className="sticky top-24 space-y-4">
              <div
                className="rounded-2xl border border-red-500/20 p-6"
                style={{
                  background: "linear-gradient(135deg, rgba(255,77,77,0.08) 0%, transparent 100%)",
                }}
              >
                <h3 className="text-red-400 font-bold text-sm uppercase tracking-wider mb-4">
                  ⚡ Ключевые факты
                </h3>
                <ul className="space-y-3">
                  {[
                    ["Длительность раунда", "от 1 до 60+ сек"],
                    ["Мин. ставка", "от 1₽"],
                    ["Макс. множитель", "100x и выше"],
                    ["RTP игры", "97%"],
                    ["Тип алгоритма", "Provably Fair"],
                    ["Одновременных ставок", "2 шт."],
                  ].map(([k, v]) => (
                    <li key={k} className="flex justify-between items-center border-b border-white/5 pb-3 last:border-0 last:pb-0">
                      <span className="text-gray-500 text-sm">{k}</span>
                      <span className="text-white font-bold text-sm">{v}</span>
                    </li>
                  ))}
                </ul>
              </div>

              <CtaButton size="md" className="w-full">
                🎮 Попробовать бесплатно
              </CtaButton>
            </div>
          </div>
        </div>
      </section>

      {/* ═══════════════════ STRATEGIES ═══════════════════ */}
      <section id="strategies" className="py-20 px-4 border-t border-white/5">
        <div className="max-w-6xl mx-auto">
          <div className="text-center mb-14">
            <div className="text-xs font-bold text-orange-400 tracking-widest uppercase mb-3">
              СОВЕТЫ ПРОФЕССИОНАЛОВ
            </div>
            <h2
              className="text-3xl md:text-5xl font-black text-white mb-4"
              style={{ fontFamily: "'Orbitron', monospace" }}
            >
              СТРАТЕГИИ ПОБЕДЫ
            </h2>
            <p className="text-gray-500 max-w-xl mx-auto">
              Нет 100% гарантированной стратегии, но эти подходы помогают управлять рисками
            </p>
          </div>

          <div className="grid md:grid-cols-3 gap-6 mb-12">
            <StrategyCard
              icon="🛡️"
              title="Консервативная"
              risk="НИЗКИЙ РИСК"
              riskColor="text-green-400 border-green-400/30"
              desc="Идеально для новичков. Частые небольшие выигрыши вместо погони за большими множителями."
              tips={[
                "Автовывод на 1.2x — 1.5x",
                "Ставить не более 2-3% от банка",
                "Не менять стратегию от эмоций",
                "Подходит для изучения ритма игры",
              ]}
            />
            <StrategyCard
              icon="⚖️"
              title="Двойная ставка"
              risk="СРЕДНИЙ РИСК"
              riskColor="text-yellow-400 border-yellow-400/30"
              desc="Используй обе панели ставок одновременно. Первая — страховка, вторая — погоня за большим."
              tips={[
                "Ставка 1: автовывод на 1.5x",
                "Ставка 2: цель 3x — 10x",
                "Первая ставка покрывает потери",
                "Гибкость в управлении риском",
              ]}
            />
            <StrategyCard
              icon="🚀"
              title="Агрессивная"
              risk="ВЫСОКИЙ РИСК"
              riskColor="text-red-400 border-red-400/30"
              desc="Охота на высокие множители. Большой потенциал, но и высокий риск потерь."
              tips={[
                "Цель: 10x — 100x",
                "Минимальные ставки при высоком риске",
                "Чёткий стоп-лосс обязателен",
                "Только с опытом игры",
              ]}
            />
          </div>

          {/* Fibonacci & Martingale */}
          <div className="grid md:grid-cols-2 gap-6">
            <div
              className="rounded-2xl border border-white/10 p-6"
              style={{ background: "linear-gradient(135deg, rgba(100,150,255,0.05) 0%, transparent 100%)" }}
            >
              <h3 className="text-lg font-black text-white mb-3 flex items-center gap-2">
                🔢 Стратегия Фибоначчи
              </h3>
              <p className="text-gray-400 text-sm leading-relaxed mb-4">
                После каждого проигрыша увеличивай ставку по последовательности: 1, 1, 2, 3, 5, 8, 13...
                После выигрыша возвращайся на два шага назад.
              </p>
              <div className="flex gap-2 flex-wrap">
                {[1, 1, 2, 3, 5, 8, 13, 21].map((n, i) => (
                  <span
                    key={i}
                    className="w-10 h-10 rounded-lg bg-blue-500/10 border border-blue-500/20 flex items-center justify-center text-blue-400 font-bold text-sm"
                  >
                    {n}
                  </span>
                ))}
              </div>
            </div>

            <div
              className="rounded-2xl border border-white/10 p-6"
              style={{ background: "linear-gradient(135deg, rgba(255,100,100,0.05) 0%, transparent 100%)" }}
            >
              <h3 className="text-lg font-black text-white mb-3 flex items-center gap-2">
                ⚡ Стратегия Мартингейл
              </h3>
              <p className="text-gray-400 text-sm leading-relaxed mb-4">
                После каждого проигрыша удваивай ставку. После выигрыша возвращайся к начальной ставке.
                <span className="text-red-400 font-semibold"> Внимание: требует большого банка!</span>
              </p>
              <div className="flex gap-2 flex-wrap">
                {[1, 2, 4, 8, 16, 32, 64].map((n, i) => (
                  <span
                    key={i}
                    className="w-10 h-10 rounded-lg bg-red-500/10 border border-red-500/20 flex items-center justify-center text-red-400 font-bold text-xs"
                  >
                    ×{n}
                  </span>
                ))}
              </div>
            </div>
          </div>

          <div className="mt-8 rounded-2xl border border-yellow-500/20 bg-yellow-500/5 p-5 flex gap-4 items-start">
            <span className="text-2xl shrink-0">⚠️</span>
            <p className="text-yellow-200/70 text-sm leading-relaxed">
              <strong className="text-yellow-400">Важно:</strong> Aviator использует алгоритм Provably Fair —
              точка краша генерируется ДО начала раунда и не зависит от ставок игроков. Ни одна стратегия
              не гарантирует выигрыш. Играй ответственно и устанавливай личные лимиты.
            </p>
          </div>
        </div>
      </section>

      {/* ═══════════════════ PROVABLY FAIR ═══════════════════ */}
      <section className="py-20 px-4 grid-bg border-t border-white/5">
        <div className="max-w-5xl mx-auto">
          <div className="grid md:grid-cols-2 gap-12 items-center">
            <div
              className="rounded-3xl border border-white/10 p-8 text-center order-2 md:order-1"
              style={{
                background: "linear-gradient(135deg, rgba(50,100,255,0.08) 0%, rgba(100,50,255,0.05) 100%)",
              }}
            >
              <div className="text-6xl mb-4">🔐</div>
              <h3 className="text-xl font-black text-white mb-4">Как работает честность?</h3>
              <div className="space-y-4 text-left">
                {[
                  { step: "1", color: "bg-blue-500", text: "Сервер генерирует зашифрованный seed до начала раунда" },
                  { step: "2", color: "bg-purple-500", text: "Клиент получает хэш seed'а для проверки" },
                  { step: "3", color: "bg-indigo-500", text: "После раунда seed раскрывается для верификации" },
                  { step: "4", color: "bg-blue-400", text: "Любой игрок может проверить честность результата" },
                ].map((s) => (
                  <div key={s.step} className="flex gap-3 items-start">
                    <div className={`w-7 h-7 rounded-full ${s.color} flex items-center justify-center text-xs font-black text-white shrink-0 mt-0.5`}>
                      {s.step}
                    </div>
                    <p className="text-gray-400 text-sm">{s.text}</p>
                  </div>
                ))}
              </div>
            </div>

            <div className="order-1 md:order-2">
              <div className="text-xs font-bold text-blue-400 tracking-widest uppercase mb-3">
                ЧЕСТНАЯ ИГРА
              </div>
              <h2
                className="text-3xl md:text-4xl font-black text-white mb-6 leading-tight"
                style={{ fontFamily: "'Orbitron', monospace" }}
              >
                PROVABLY{" "}
                <span className="text-blue-400">FAIR</span>
              </h2>
              <p className="text-gray-400 leading-relaxed mb-6">
                Aviator использует революционную технологию <strong className="text-white">Provably Fair</strong> —
                это означает, что ни казино, ни разработчик не могут повлиять на результат раунда.
              </p>
              <p className="text-gray-400 leading-relaxed mb-8">
                Точка краша определяется криптографическим алгоритмом ещё до того, как раунд начался.
                Это гарантирует абсолютную честность каждого полёта.
              </p>
              <div className="grid grid-cols-2 gap-4">
                {[
                  { icon: "🎲", label: "100% случайность" },
                  { icon: "🔍", label: "Проверяемость" },
                  { icon: "🚫", label: "Без манипуляций" },
                  { icon: "✅", label: "Независимый аудит" },
                ].map((f) => (
                  <div
                    key={f.label}
                    className="flex items-center gap-3 rounded-xl border border-white/10 bg-white/3 p-3"
                  >
                    <span className="text-xl">{f.icon}</span>
                    <span className="text-sm font-semibold text-white">{f.label}</span>
                  </div>
                ))}
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* ═══════════════════ BIG CTA ═══════════════════ */}
      <section className="py-20 px-4 relative overflow-hidden border-t border-white/5">
        <div
          className="absolute inset-0 pointer-events-none"
          style={{
            background: "radial-gradient(ellipse at center, rgba(255,77,77,0.15) 0%, transparent 70%)",
          }}
        />
        <div className="relative max-w-3xl mx-auto text-center">
          <img
            src={LOGO_URL}
            alt="Aviator"
            className="h-24 w-auto mx-auto mb-6 object-contain drop-shadow-[0_0_30px_rgba(255,150,0,0.5)]"
            style={{ animation: "planeMove 4s ease-in-out infinite" }}
          />
          <h2
            className="text-3xl md:text-5xl font-black text-white mb-4"
            style={{ fontFamily: "'Orbitron', monospace" }}
          >
            ГОТОВ ВЗЛЕТЕТЬ?
          </h2>
          <p className="text-gray-400 text-lg mb-8">
            Присоединись к миллионам игроков. Первый депозит — бонус до 200%!
          </p>
          <CtaButton size="lg" className="mb-4">
            🚀 НАЧАТЬ ИГРАТЬ СЕЙЧАС
          </CtaButton>
          <p className="text-gray-600 text-xs mt-4">
            18+ | Играй ответственно | Условия применяются
          </p>
        </div>
      </section>

      {/* ═══════════════════ TIPS FOR BEGINNERS ═══════════════════ */}
      <section className="py-20 px-4 border-t border-white/5">
        <div className="max-w-5xl mx-auto">
          <div className="text-center mb-14">
            <div className="text-xs font-bold text-green-400 tracking-widest uppercase mb-3">
              СОВЕТЫ
            </div>
            <h2
              className="text-3xl md:text-4xl font-black text-white mb-4"
              style={{ fontFamily: "'Orbitron', monospace" }}
            >
              СОВЕТЫ ДЛЯ НОВИЧКОВ
            </h2>
          </div>

          <div className="grid sm:grid-cols-2 lg:grid-cols-3 gap-5">
            {[
              {
                icon: "🎯",
                title: "Начни с демо",
                desc: "Перед игрой на реальные деньги освой механику в режиме демо. Это бесплатно и поможет понять ритм игры.",
              },
              {
                icon: "💰",
                title: "Управляй банком",
                desc: "Ставь не более 1-3% от общего банка за раунд. Установи дневной лимит потерь и строго его соблюдай.",
              },
              {
                icon: "🤖",
                title: "Используй автовывод",
                desc: "Функция автоматического снятия на заданном множителе спасает от эмоциональных решений в горячий момент.",
              },
              {
                icon: "📊",
                title: "Изучай историю",
                desc: "В игре отображается история предыдущих раундов. Анализируй паттерны, но помни — каждый раунд независим.",
              },
              {
                icon: "🧘",
                title: "Оставайся спокойным",
                desc: "Не гонись за потерями и не играй на эмоциях. Дисциплина — главное оружие успешного игрока.",
              },
              {
                icon: "🎁",
                title: "Используй бонусы",
                desc: "Воспользуйся приветственным бонусом казино для увеличения банка. Читай условия отыгрыша внимательно.",
              },
            ].map((tip) => (
              <div
                key={tip.title}
                className="rounded-2xl border border-white/10 bg-white/3 hover:bg-white/5 hover:border-white/20 transition-all duration-300 p-5"
              >
                <div className="text-3xl mb-3">{tip.icon}</div>
                <h3 className="font-bold text-white mb-2">{tip.title}</h3>
                <p className="text-gray-500 text-sm leading-relaxed">{tip.desc}</p>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* ═══════════════════ REVIEWS ═══════════════════ */}
      <section id="reviews" className="py-20 px-4 grid-bg border-t border-white/5">
        <div className="max-w-5xl mx-auto">
          <div className="text-center mb-14">
            <div className="text-xs font-bold text-yellow-400 tracking-widest uppercase mb-3">
              ОТЗЫВЫ
            </div>
            <h2
              className="text-3xl md:text-4xl font-black text-white mb-4"
              style={{ fontFamily: "'Orbitron', monospace" }}
            >
              ЧТО ГОВОРЯТ ИГРОКИ
            </h2>
            <div className="flex justify-center gap-1 mb-2">
              {[...Array(5)].map((_, i) => (
                <span key={i} className="text-yellow-400 text-xl">★</span>
              ))}
            </div>
            <p className="text-gray-500 text-sm">4.8/5 на основе 12,000+ отзывов</p>
          </div>

          <div className="grid md:grid-cols-3 gap-5">
            <Testimonial
              name="Александр К."
              stars={5}
              win="+48,000₽"
              text="Играю уже 8 месяцев. Стратегия с двойной ставкой реально работает! Главное — дисциплина. Снял 48к за выходные."
            />
            <Testimonial
              name="Мария В."
              stars={5}
              win="+12,500₽"
              text="Поначалу скептически относилась, но теперь поняла механику. Автовывод на 1.5x — мой лучший друг. Стабильный плюс каждую неделю."
            />
            <Testimonial
              name="Дмитрий Н."
              stars={5}
              win="+89,000₽"
              text="Поймал множитель 18.7x! Это было нереально. Конечно, не каждый день такое, но и 2-3x приходят регулярно. Советую всем!"
            />
            <Testimonial
              name="Анна С."
              stars={4}
              win="+6,200₽"
              text="Честная игра, быстрые выплаты. Иногда везёт меньше, но в целом доволен. Интерфейс очень удобный."
            />
            <Testimonial
              name="Сергей М."
              stars={5}
              win="+31,000₽"
              text="Играю по стратегии Фибоначчи с автовыводом на 2x. Месяц в плюсе на 31 тысячу. Главное — не жадничать!"
            />
            <Testimonial
              name="Елена Р."
              stars={5}
              win="+15,800₽"
              text="Попробовала на демо, потом зашла на реальные. Уже второй месяц в плюсе. Игра честная, проверяла через провабли фэа."
            />
          </div>
        </div>
      </section>

      {/* ═══════════════════ FAQ ═══════════════════ */}
      <section id="faq" className="py-20 px-4 border-t border-white/5">
        <div className="max-w-3xl mx-auto">
          <div className="text-center mb-14">
            <div className="text-xs font-bold text-purple-400 tracking-widest uppercase mb-3">
              ВОПРОСЫ И ОТВЕТЫ
            </div>
            <h2
              className="text-3xl md:text-4xl font-black text-white mb-4"
              style={{ fontFamily: "'Orbitron', monospace" }}
            >
              ЧАСТЫЕ ВОПРОСЫ
            </h2>
          </div>

          <div className="space-y-3">
            {[
              {
                q: "Можно ли выиграть реальные деньги в Aviator?",
                a: "Да! Aviator — это реальная игра на деньги в лицензированных онлайн-казино. Выигрыши выплачиваются мгновенно на банковские карты, электронные кошельки или криптовалютные счета.",
              },
              {
                q: "Что такое Provably Fair и почему это важно?",
                a: "Provably Fair (Доказуемо честный) — это технология, при которой результат каждого раунда генерируется криптографическим алгоритмом ещё ДО начала игры. Ни казино, ни провайдер не могут изменить результат. Вы можете самостоятельно верифицировать каждый раунд.",
              },
              {
                q: "Какой максимальный множитель в Aviator?",
                a: "Теоретически самолёт может достичь 100x и даже выше. Однако такие высокие множители встречаются очень редко. Большинство раундов завершается на множителях от 1.2x до 5x.",
              },
              {
                q: "Есть ли стратегия, гарантирующая выигрыш?",
                a: "Нет! Aviator использует Random Number Generator (RNG) + Provably Fair алгоритм. Каждый раунд абсолютно случаен и независим. Никакая стратегия не даёт гарантий, но правильное управление банком снижает риски.",
              },
              {
                q: "Можно ли играть бесплатно?",
                a: "Да, большинство казино предлагают демо-режим, где можно играть без риска. Это отличный способ изучить механику игры, отработать стратегии и понять ритм раундов.",
              },
              {
                q: "Сколько ставок можно сделать за раунд?",
                a: "В Aviator вы можете делать одновременно ДВЕ ставки в одном раунде. Это позволяет комбинировать консервативную и агрессивную стратегии — одна ставка страхует, другая охотится за большим множителем.",
              },
              {
                q: "Как работает функция автовывода?",
                a: "Вы заранее устанавливаете целевой множитель (например, 2.0x). Когда самолёт достигает этого значения, ставка снимается автоматически — даже если вы не успели нажать кнопку вручную. Очень полезная функция для дисциплинированной игры.",
              },
              {
                q: "Какой минимальный депозит для игры?",
                a: "Минимальный депозит зависит от конкретного казино, но обычно составляет от 100₽. Минимальная ставка в самой игре может начинаться от 1₽.",
              },
            ].map((item) => (
              <FaqItem key={item.q} {...item} />
            ))}
          </div>
        </div>
      </section>

      {/* ═══════════════════ FINAL CTA ═══════════════════ */}
      <section className="py-20 px-4 relative overflow-hidden border-t border-white/5">
        <div
          className="absolute inset-0 pointer-events-none"
          style={{
            background:
              "linear-gradient(180deg, transparent 0%, rgba(255,77,77,0.08) 50%, transparent 100%)",
          }}
        />
        <Particles />
        <div className="relative max-w-4xl mx-auto">
          <div
            className="rounded-3xl border border-red-500/20 p-10 md:p-16 text-center glow-red"
            style={{
              background:
                "linear-gradient(135deg, rgba(255,77,77,0.08) 0%, rgba(255,153,0,0.05) 50%, rgba(0,0,0,0.5) 100%)",
            }}
          >
            <img
              src={LOGO_URL}
              alt="Aviator"
              className="h-20 w-auto mx-auto mb-6 object-contain drop-shadow-[0_0_40px_rgba(255,150,0,0.6)]"
              style={{ animation: "planeMove 4s ease-in-out infinite" }}
            />
            <h2
              className="text-3xl md:text-5xl font-black mb-4"
              style={{ fontFamily: "'Orbitron', monospace" }}
            >
              <span className="shimmer-text">ВЗЛЕТАЙ ПРЯМО СЕЙЧАС!</span>
            </h2>
            <p className="text-gray-400 text-lg mb-10 max-w-xl mx-auto">
              Более <strong className="text-white">47,000 игроков</strong> сейчас онлайн.
              Не упусти свой шанс на большой выигрыш!
            </p>
            <div className="flex flex-col sm:flex-row gap-4 justify-center">
              <CtaButton size="lg">
                ✈️ ИГРАТЬ В AVIATOR
              </CtaButton>
            </div>
            <div className="mt-8 flex flex-wrap justify-center gap-6 text-sm text-gray-600">
              <span>🔒 Безопасно</span>
              <span>⚡ Мгновенные выплаты</span>
              <span>🎁 Бонус на депозит</span>
              <span>📱 Мобильная версия</span>
            </div>
          </div>
        </div>
      </section>

      {/* ═══════════════════ FOOTER ═══════════════════ */}
      <footer className="border-t border-white/10 py-10 px-4">
        <div className="max-w-5xl mx-auto">
          <div className="flex flex-col md:flex-row items-center justify-between gap-6 mb-8">
            <div className="flex items-center gap-3">
              <img src={LOGO_URL} alt="Aviator" className="h-8 w-auto object-contain" />
              <span
                className="font-black text-white"
                style={{ fontFamily: "'Orbitron', monospace" }}
              >
                AVIATOR
              </span>
            </div>
            <div className="flex flex-wrap justify-center gap-6 text-sm text-gray-500">
              <a href={CASINO_LINK} target="_blank" rel="noopener noreferrer" className="hover:text-white transition-colors">
                Играть
              </a>
              <button onClick={() => scrollTo("howto")} className="hover:text-white transition-colors">
                Как играть
              </button>
              <button onClick={() => scrollTo("strategies")} className="hover:text-white transition-colors">
                Стратегии
              </button>
              <button onClick={() => scrollTo("faq")} className="hover:text-white transition-colors">
                FAQ
              </button>
            </div>
          </div>

          <div className="border-t border-white/5 pt-6 text-center space-y-3">
            <p className="text-gray-600 text-xs leading-relaxed max-w-2xl mx-auto">
              ⚠️ Данный сайт предназначен только для лиц старше <strong>18 лет</strong>.
              Азартные игры несут риск потери денег. Играйте ответственно.
              Если вы чувствуете зависимость — обратитесь за помощью.
            </p>
            <p className="text-gray-700 text-xs">
              © 2025 Aviator Guide. Все права защищены. Информационный сайт.
            </p>
          </div>
        </div>
      </footer>
    </div>
  );
}
