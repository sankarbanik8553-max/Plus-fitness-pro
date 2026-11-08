```react
import React, { useState, useEffect } from "react";
import {
  Dumbbell,
  Users,
  Trophy,
  Clock,
  CheckCircle2,
  Play,
  ArrowRight,
  Phone,
  Mail,
  MapPin,
  Instagram,
  Facebook,
  Twitter,
  Linkedin,
  MessageCircle,
  Menu,
  X,
  ChevronUp,
  Star,
  Activity,
  Flame,
  ChevronRight,
  Maximize2,
  Trash2,
  Edit,
  TrendingUp,
  UserCheck,
  Settings,
  Plus,
  Shield,
  Zap,
  Award,
  HeartPulse,
  Calendar,
  Filter,
  Check,
  Search,
  Sparkles
} from "lucide-react";

// ==========================================
// CENTRAL CONFIGURATION & DEMO DATA SYSTEM
// ==========================================
const CONFIG = {
  brandName: "PULSE",
  brandTagline: "Stronger • Fitter • Healthier",
  contact: {
    phone: "+91 98765 43210",
    email: "info@pulsefitness-demo.com",
    address: "123 Fitness Street, Central Avenue, City, 10001",
    whatsapp: "919876543210"
  },
  colors: {
    bgPrimary: "#080808",
    bgSecondary: "#141414",
    bgCard: "#1A1A1A",
    accent: "#FF303B",
    textPrimary: "#FFFFFF",
    textSecondary: "#B5B5B5"
  }
};

const STATS_DATA = [
  { icon: Users, value: "1,200+", label: "Active Athletes" },
  { icon: Star, value: "4.9 / 5.0", label: "Client Rating" },
  { icon: Trophy, value: "100%", label: "Result Guaranteed" },
  { icon: Clock, value: "24/7", label: "Facility Access" }
];

const PROGRAMS_DATA = [
  {
    id: "strength",
    category: "strength",
    title: "Strength & Powerlifting",
    desc: "Build elite compound power, muscle mass, and structural density with heavy barbell setups and progressive overload protocols.",
    image: "https://images.unsplash.com/photo-1534438327276-14e5300c3a48?auto=format&fit=crop&q=80&w=800",
    benefits: ["Hypertrophy focus", "Free weights & Racks", "1-on-1 Spotting & Form Audits"],
    intensity: "High"
  },
  {
    id: "cardio",
    category: "cardio",
    title: "Cardio & High Intensity HIIT",
    desc: "High-intensity interval training designed to skyrocket cardiovascular endurance, shred body fat, and optimize stamina.",
    image: "https://images.unsplash.com/photo-1517838277536-f5f99be501cd?auto=format&fit=crop&q=80&w=800",
    benefits: ["Metabolic Acceleration", "Real-Time HR Tracking", "High Caloric Afterburn"],
    intensity: "Extreme"
  },
  {
    id: "functional",
    category: "functional",
    title: "Functional & Cross Conditioning",
    desc: "Dynamic multi-planar movements using kettlebells, battle ropes, and plyometrics for real-world athletic agility and core stability.",
    image: "https://images.unsplash.com/photo-1541534741688-6078c6bfb5c5?auto=format&fit=crop&q=80&w=800",
    benefits: ["Kettlebell Workouts", "TRX & Suspension Systems", "Agility & Speed Drills"],
    intensity: "Moderate-High"
  },
  {
    id: "muscle",
    category: "strength",
    title: "Hypertrophy Bodybuilding",
    desc: "Targeted isolation routines and metabolic stress techniques engineered specifically for symmetrical muscular hypertrophy.",
    image: "https://images.unsplash.com/photo-1583454110551-21f2fa2afe61?auto=format&fit=crop&q=80&w=800",
    benefits: ["Targeted Isolation Drills", "Custom Macro Meal Plans", "Posing & Aesthetic Guidance"],
    intensity: "High"
  },
  {
    id: "mobility",
    category: "mobility",
    title: "Flexibility & Postural Yoga",
    desc: "Restore joint mechanics, decompress spinal vertebrae, and increase active range-of-motion to accelerate muscle recovery.",
    image: "https://images.unsplash.com/photo-1518611012118-696072aa579a?auto=format&fit=crop&q=80&w=800",
    benefits: ["Injury Prevention", "Active Recovery", "Breath Control & Core Dynamics"],
    intensity: "Low-Moderate"
  },
  {
    id: "personal",
    category: "personal",
    title: "1-on-1 Elite Personal Coaching",
    desc: "Tailored bio-individual fitness blueprints, daily nutrition tracking, and dedicated custom workouts under master coaches.",
    image: "https://images.unsplash.com/photo-1571019613454-1cb2f99b2d8b?auto=format&fit=crop&q=80&w=800",
    benefits: ["Dedicated Master Coach", "Custom Meal Protocols", "Weekly Body Composition Analytics"],
    intensity: "Custom"
  }
];

const TRAINERS_DATA = [
  {
    id: "1",
    name: "Alex Johnson",
    role: "Head Strength & Conditioning",
    exp: "8+ Years Experience",
    spec: "Powerlifting & Bodybuilding",
    bio: "Certified CSCS strength strategist specializing in compound powerlifting and high-yield muscular hypertrophy.",
    image: "https://images.unsplash.com/photo-1567013127542-490d757e51fc?auto=format&fit=crop&q=80&w=600"
  },
  {
    id: "2",
    name: "Priya Sharma",
    role: "Functional Performance Coach",
    exp: "6+ Years Experience",
    spec: "HIIT & Kinetic Mobility",
    bio: "Former national sprint athlete coaching members in high-output metabolic conditioning and dynamic core strength.",
    image: "https://images.unsplash.com/photo-1573496359142-b8d87734a5a2?auto=format&fit=crop&q=80&w=600"
  },
  {
    id: "3",
    name: "Rahul Mehta",
    role: "Tactical Combat & Endurance Lead",
    exp: "7+ Years Experience",
    spec: "Kickboxing & Cross Training",
    bio: "Focuses on explosive movement, tactical body re-composition, and high-energy athletic stamina routines.",
    image: "https://images.unsplash.com/photo-1534528741775-53994a69daeb?auto=format&fit=crop&q=80&w=600"
  },
  {
    id: "4",
    name: "Sneha Roy",
    role: "Postural & Mobility Director",
    exp: "5+ Years Experience",
    spec: "Rehabilitation & Yoga",
    bio: "Specialist in resolving joint restrictions, restoring postural alignment, and optimizing natural recovery.",
    image: "https://images.unsplash.com/photo-1544005313-94ddf0286df2?auto=format&fit=crop&q=80&w=600"
  }
];

const MEMBERSHIP_PLANS = [
  {
    name: "Basic Plan",
    monthlyPrice: 999,
    isPopular: false,
    desc: "Essential gym floor access for consistent self-directed athletes.",
    features: [
      "Standard Gym Floor & Weight Access",
      "Locker Room & Shower Access",
      "Basic Fitness Orientation Session",
      "PULSE Mobile App Workout Tracker"
    ]
  },
  {
    name: "Pro Plan",
    monthlyPrice: 1499,
    isPopular: true,
    desc: "Our recommended package for dedicated fitness enthusiasts looking for guidance.",
    features: [
      "All Basic Plan Privileges",
      "Full Sauna & Steam Bath Access",
      "2 Monthly Personal Coach Sessions",
      "Custom Macro Nutrition Blueprint",
      "Priority Group Fitness Reservations"
    ]
  },
  {
    name: "Premium Plan",
    monthlyPrice: 1999,
    isPopular: false,
    desc: "The ultimate VIP all-inclusive athletic access tier with dedicated coaching.",
    features: [
      "All Pro Plan Privileges",
      "Unlimited 1-on-1 Master Coaching",
      "Dedicated Permanent Personal Locker",
      "Complimentary Shake & Hydration Bar",
      "3 Guest Access Passes Per Month"
    ]
  }
];

const GALLERY_IMAGES = [
  { id: 1, title: "Main Olympic Lifting Platforms", category: "strength", src: "https://images.unsplash.com/photo-1534438327276-14e5300c3a48?auto=format&fit=crop&q=80&w=800" },
  { id: 2, title: "Cardio & Stamina Arena", category: "cardio", src: "https://images.unsplash.com/photo-1576678927484-cc907957088c?auto=format&fit=crop&q=80&w=800" },
  { id: 3, title: "Synthetic Functional Turf Area", category: "functional", src: "https://images.unsplash.com/photo-1541534741688-6078c6bfb5c5?auto=format&fit=crop&q=80&w=800" },
  { id: 4, title: "Hydrotherapy & Recovery Sauna", category: "facilities", src: "https://images.unsplash.com/photo-1540555700478-4be289fbecef?auto=format&fit=crop&q=80&w=800" },
  { id: 5, title: "Heavy Dumbbell & Dumbbell Zone", category: "strength", src: "https://images.unsplash.com/photo-1526506118085-60ce8714f8c5?auto=format&fit=crop&q=80&w=800" },
  { id: 6, title: "Group Mobility & Yoga Studio", category: "facilities", src: "https://images.unsplash.com/photo-1518611012118-696072aa579a?auto=format&fit=crop&q=80&w=800" }
];

const INITIAL_SCHEDULE = [
  { time: "06:00 AM - 07:00 AM", mon: "Strength", tue: "HIIT", wed: "Strength", thu: "HIIT", fri: "Strength", sat: "Cardio", sun: "Rest" },
  { time: "08:00 AM - 09:00 AM", mon: "Yoga", tue: "CrossFit", wed: "Yoga", thu: "CrossFit", fri: "Yoga", sat: "Mobility", sun: "Rest" },
  { time: "05:00 PM - 06:00 PM", mon: "Cardio", tue: "Strength", wed: "Cardio", thu: "Strength", fri: "Cardio", sat: "HIIT", sun: "Rest" },
  { time: "07:00 PM - 08:00 PM", mon: "Combat", tue: "Functional", wed: "Combat", thu: "Functional", fri: "Combat", sat: "Strength", sun: "Rest" }
];

const REVIEWS_DATA = [
  { name: "Vikram Malhotra", role: "Software Architect", comment: "The bi-mechanic equipment is world-class. I gained 7kg of lean muscle mass in 5 months under Alex's coaching schedule!", rating: 5 },
  { name: "Ananya Deshmukh", role: "Creative Director", comment: "Spacious layout, zero waiting for racks during peak hours, and super clean hydromassage amenities. Worth every rupee.", rating: 5 },
  { name: "Rohan Gupta", role: "Tech Founder", comment: "The Pro plan personalized diet and strength coaching changed my energy levels completely. Best fitness venue in the city.", rating: 5 }
];

const FAQS_DATA = [
  { q: "What are your facility operating hours?", a: "We are open 24/7 for Premium tier members. General floor access runs Monday–Saturday 5:00 AM – 11:00 PM and Sunday 6:00 AM – 9:00 PM." },
  { q: "Do you offer a trial pass before commitment?", a: "Yes! We provide a complimentary 1-Day VIP Pass allowing full access to equipment and trial classes." },
  { q: "Can I pause or freeze my membership while traveling?", a: "Yes, memberships can be paused up to 30 days per calendar year on Pro and Premium subscription tiers." },
  { q: "Are personal coaches included with basic membership?", a: "Basic members receive an initial orientation. Dedicated 1-on-1 personal coaching is included in Pro & Premium tiers." }
];

// ==========================================
// MAIN APPLICATION COMPONENT
// ==========================================
export default function App() {
  const [currentPage, setCurrentPage] = useState("home");
  const [mobileMenuOpen, setMobileMenuOpen] = useState(false);
  const [scrolled, setScrolled] = useState(false);
  const [billingCycle, setBillingCycle] = useState("monthly");
  const [selectedImage, setSelectedImage] = useState(null);
  const [modalOpen, setModalOpen] = useState(false);
  const [modalType, setModalType] = useState("join");
  const [showScrollTop, setShowScrollTop] = useState(false);
  const [scheduleData, setScheduleData] = useState(INITIAL_SCHEDULE);

  // Form State
  const [formData, setFormData] = useState({ name: "", email: "", phone: "", plan: "Pro Plan", notes: "" });
  const [formSuccess, setFormSuccess] = useState(false);

  // FAQ Accordion State
  const [openFaq, setOpenFaq] = useState(0);

  // Admin Dashboard Lead Enquiries State
  const [enquiries, setEnquiries] = useState([
    { id: 101, name: "Karan Johar", email: "karan@example.com", phone: "+91 98200 11223", plan: "Pro Plan", status: "Pending", date: "2026-11-07" },
    { id: 102, name: "Simran Kaur", email: "simran@example.com", phone: "+91 98111 44556", plan: "Premium Plan", status: "Contacted", date: "2026-11-06" },
    { id: 103, name: "Amitabh Roy", email: "roy@example.com", phone: "+91 97654 32109", plan: "Basic Plan", status: "Trial Scheduled", date: "2026-11-05" }
  ]);

  useEffect(() => {
    const handleScroll = () => {
      setScrolled(window.scrollY > 30);
      setShowScrollTop(window.scrollY > 350);
    };
    window.addEventListener("scroll", handleScroll);
    return () => window.removeEventListener("scroll", handleScroll);
  }, []);

  const navigateTo = (page) => {
    setCurrentPage(page);
    setMobileMenuOpen(false);
    window.scrollTo({ top: 0, behavior: "smooth" });
  };

  const openBookingModal = (type) => {
    setModalType(type);
    setFormSuccess(false);
    setModalOpen(true);
  };

  const handleFormSubmit = (e) => {
    e.preventDefault();
    if (!formData.name || !formData.phone) return;
    setFormSuccess(true);
    setEnquiries([
      {
        id: Date.now(),
        name: formData.name,
        email: formData.email || "N/A",
        phone: formData.phone,
        plan: formData.plan,
        status: "Pending",
        date: new Date().toISOString().split("T")[0]
      },
      ...enquiries
    ]);
    setTimeout(() => {
      setModalOpen(false);
      setFormSuccess(false);
      setFormData({ name: "", email: "", phone: "", plan: "Pro Plan", notes: "" });
    }, 2000);
  };

  const calculatePrice = (monthly) => {
    if (billingCycle === "quarterly") return Math.round(monthly * 0.9);
    if (billingCycle === "yearly") return Math.round(monthly * 0.8);
    return monthly;
  };

  return (
    <div className="min-h-screen bg-[#080808] text-white font-sans antialiased selection:bg-[#FF303B] selection:text-white relative">
      
      {/* ------------------------------------
          NAVBAR COMPONENT
      ------------------------------------ */}
      <header
        className={`fixed top-0 left-0 right-0 z-50 transition-all duration-300 border-b ${
          scrolled ? "bg-[#080808]/95 backdrop-blur-md border-[#1A1A1A] py-3 shadow-xl" : "bg-transparent border-transparent py-5"
        }`}
      >
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex items-center justify-between">
          
          {/* Logo */}
          <div
            onClick={() => navigateTo("home")}
            className="flex items-center gap-2.5 cursor-pointer group"
          >
            <div className="w-10 h-10 bg-[#FF303B] rounded-xl flex items-center justify-center transform group-hover:rotate-6 transition-transform shadow-lg shadow-[#FF303B]/20">
              <Dumbbell className="w-6 h-6 text-white" />
            </div>
            <div>
              <span className="text-2xl font-black tracking-widest text-white uppercase block leading-none">
                {CONFIG.brandName}
              </span>
              <span className="text-[10px] text-[#B5B5B5] tracking-widest uppercase font-semibold">
                Fitness Club
              </span>
            </div>
          </div>

          {/* Desktop Navigation Links */}
          <nav className="hidden lg:flex items-center gap-6">
            {[
              { id: "home", label: "Home" },
              { id: "about", label: "About" },
              { id: "programs", label: "Programs" },
              { id: "membership", label: "Membership" },
              { id: "trainers", label: "Trainers" },
              { id: "gallery", label: "Gallery" },
              { id: "schedule", label: "Schedule" },
              { id: "reviews", label: "Reviews" },
              { id: "contact", label: "Contact" }
            ].map((link) => (
              <button
                key={link.id}
                onClick={() => navigateTo(link.id)}
                className={`text-xs font-bold transition-colors duration-200 uppercase tracking-wider relative py-1 ${
                  currentPage === link.id ? "text-[#FF303B]" : "text-[#B5B5B5] hover:text-white"
                }`}
              >
                {link.label}
                {currentPage === link.id && (
                  <span className="absolute bottom-0 left-0 right-0 h-0.5 bg-[#FF303B] rounded-full"></span>
                )}
              </button>
            ))}
          </nav>

          {/* Action Header Buttons */}
          <div className="hidden lg:flex items-center gap-3">
            <button
              onClick={() => navigateTo("admin")}
              className="text-xs text-[#B5B5B5] hover:text-white transition-colors flex items-center gap-1.5 border border-[#1A1A1A] bg-[#141414] px-3 py-2 rounded-lg"
              title="Demo Admin Dashboard"
            >
              <Settings className="w-3.5 h-3.5 text-[#FF303B]" />
              <span>Admin Demo</span>
            </button>
            <button
              onClick={() => openBookingModal("join")}
              className="bg-[#FF303B] hover:bg-[#e02630] text-white text-xs font-black px-5 py-2.5 rounded-lg uppercase tracking-wider transition-all shadow-lg shadow-[#FF303B]/30 hover:shadow-[#FF303B]/50 hover:-translate-y-0.5 flex items-center gap-2"
            >
              <span>Join Now</span>
              <ArrowRight className="w-4 h-4" />
            </button>
          </div>

          {/* Mobile Navigation Toggle */}
          <div className="flex lg:hidden items-center gap-2">
            <button
              onClick={() => navigateTo("admin")}
              className="px-2.5 py-1.5 border border-[#1A1A1A] bg-[#141414] text-[11px] font-bold text-[#FF303B] rounded-md"
            >
              Admin
            </button>
            <button
              onClick={() => setMobileMenuOpen(!mobileMenuOpen)}
              className="p-2 text-[#B5B5B5] hover:text-white focus:outline-none"
            >
              {mobileMenuOpen ? <X className="w-7 h-7" /> : <Menu className="w-7 h-7" />}
            </button>
          </div>
        </div>

        {/* Mobile Navigation Drawer */}
        {mobileMenuOpen && (
          <div className="lg:hidden bg-[#141414] border-b border-[#1A1A1A] px-4 pt-4 pb-6 space-y-2">
            {[
              { id: "home", label: "Home" },
              { id: "about", label: "About" },
              { id: "programs", label: "Programs" },
              { id: "membership", label: "Membership" },
              { id: "trainers", label: "Trainers" },
              { id: "gallery", label: "Gallery & Facilities" },
              { id: "schedule", label: "Schedule" },
              { id: "reviews", label: "Reviews" },
              { id: "contact", label: "Contact" },
              { id: "admin", label: "Admin Dashboard Prototype" }
            ].map((link) => (
              <button
                key={link.id}
                onClick={() => navigateTo(link.id)}
                className={`block w-full text-left px-3 py-2 rounded-lg text-sm font-bold uppercase tracking-wider ${
                  currentPage === link.id ? "bg-[#FF303B] text-white" : "text-[#B5B5B5] hover:bg-[#1A1A1A] hover:text-white"
                }`}
              >
                {link.label}
              </button>
            ))}
            <button
              onClick={() => openBookingModal("join")}
              className="w-full bg-[#FF303B] text-white font-black py-3 rounded-lg text-center uppercase tracking-wider text-xs shadow-lg mt-3"
            >
              Join Membership Now
            </button>
          </div>
        )}
      </header>

      {/* ------------------------------------
          PAGE ROUTER RENDERER
      ------------------------------------ */}
      <main className="pt-20">
        {currentPage === "home" && (
          <HomePage
            navigateTo={navigateTo}
            openBookingModal={openBookingModal}
            setSelectedImage={setSelectedImage}
            billingCycle={billingCycle}
            setBillingCycle={setBillingCycle}
            calculatePrice={calculatePrice}
            openFaq={openFaq}
            setOpenFaq={setOpenFaq}
            scheduleData={scheduleData}
          />
        )}

        {currentPage === "about" && <AboutPage openBookingModal={openBookingModal} />}
        {currentPage === "programs" && <ProgramsPage openBookingModal={openBookingModal} />}
        {currentPage === "trainers" && <TrainersPage openBookingModal={openBookingModal} />}
        {currentPage === "membership" && (
          <MembershipPage
            billingCycle={billingCycle}
            setBillingCycle={setBillingCycle}
            calculatePrice={calculatePrice}
            openBookingModal={openBookingModal}
            openFaq={openFaq}
            setOpenFaq={setOpenFaq}
          />
        )}
        {currentPage === "gallery" && <GalleryPage setSelectedImage={setSelectedImage} />}
        {currentPage === "schedule" && (
          <SchedulePage scheduleData={scheduleData} openBookingModal={openBookingModal} />
        )}
        {currentPage === "reviews" && <ReviewsPage openBookingModal={openBookingModal} />}
        {currentPage === "contact" && <ContactPage />}
        {currentPage === "admin" && (
          <AdminDashboard
            enquiries={enquiries}
            setEnquiries={setEnquiries}
            scheduleData={scheduleData}
            setScheduleData={setScheduleData}
          />
        )}
      </main>

      {/* ------------------------------------
          FOOTER COMPONENT
      ------------------------------------ */}
      <footer className="bg-[#141414] border-t border-[#1A1A1A] pt-16 pb-8">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-10 mb-12">
            
            {/* Brand Information */}
            <div className="space-y-4">
              <div className="flex items-center gap-2.5">
                <div className="w-9 h-9 bg-[#FF303B] rounded-lg flex items-center justify-center">
                  <Dumbbell className="w-5 h-5 text-white" />
                </div>
                <span className="text-xl font-black tracking-widest text-white uppercase">
                  {CONFIG.brandName}
                </span>
              </div>
              <p className="text-[#B5B5B5] text-xs leading-relaxed">
                Transform your physique and athletic conditioning with expert master coaching, bio-mechanic equipment, and an elite gym community.
              </p>
              <div className="flex items-center gap-3 pt-2">
                {[Instagram, Facebook, Twitter, Linkedin].map((Icon, idx) => (
                  <a
                    key={idx}
                    href="#"
                    onClick={(e) => e.preventDefault()}
                    className="w-9 h-9 rounded-lg bg-[#1A1A1A] border border-white/5 flex items-center justify-center text-[#B5B5B5] hover:text-[#FF303B] hover:border-[#FF303B]/40 transition-colors"
                  >
                    <Icon className="w-4 h-4" />
                  </a>
                ))}
              </div>
            </div>

            {/* Quick Links */}
            <div>
              <h3 className="text-white font-bold text-xs tracking-widest uppercase mb-4 border-l-2 border-[#FF303B] pl-2.5">
                Quick Navigation
              </h3>
              <ul className="space-y-2 text-xs text-[#B5B5B5]">
                {["Home", "About", "Programs", "Membership", "Trainers", "Gallery", "Schedule"].map((item) => (
                  <li key={item}>
                    <button
                      onClick={() => navigateTo(item.toLowerCase())}
                      className="hover:text-[#FF303B] transition-colors flex items-center gap-1.5 uppercase font-medium"
                    >
                      <ChevronRight className="w-3.5 h-3.5 text-[#FF303B]" />
                      <span>{item}</span>
                    </button>
                  </li>
                ))}
              </ul>
            </div>

            {/* Contact Details */}
            <div>
              <h3 className="text-white font-bold text-xs tracking-widest uppercase mb-4 border-l-2 border-[#FF303B] pl-2.5">
                Club Location & Hours
              </h3>
              <ul className="space-y-3 text-xs text-[#B5B5B5]">
                <li className="flex items-start gap-2.5">
                  <MapPin className="w-4 h-4 text-[#FF303B] shrink-0 mt-0.5" />
                  <span>{CONFIG.contact.address}</span>
                </li>
                <li className="flex items-center gap-2.5">
                  <Phone className="w-4 h-4 text-[#FF303B] shrink-0" />
                  <span>{CONFIG.contact.phone}</span>
                </li>
                <li className="flex items-center gap-2.5">
                  <Mail className="w-4 h-4 text-[#FF303B] shrink-0" />
                  <span>{CONFIG.contact.email}</span>
                </li>
              </ul>
            </div>

            {/* Newsletter Subscription */}
            <div>
              <h3 className="text-white font-bold text-xs tracking-widest uppercase mb-4 border-l-2 border-[#FF303B] pl-2.5">
                Athletic Newsletter
              </h3>
              <p className="text-xs text-[#B5B5B5] mb-3">
                Subscribe for workout blueprints, macro advice, and club announcements.
              </p>
              <form onSubmit={(e) => { e.preventDefault(); alert("Subscribed to workout newsletter!"); }} className="space-y-2">
                <input
                  type="email"
                  placeholder="Enter email address"
                  required
                  className="w-full bg-[#1A1A1A] border border-white/10 rounded-lg px-3.5 py-2.5 text-xs text-white placeholder-[#B5B5B5] focus:outline-none focus:border-[#FF303B]"
                />
                <button
                  type="submit"
                  className="w-full bg-[#FF303B] hover:bg-[#e02630] text-white font-bold py-2.5 rounded-lg text-xs uppercase tracking-wider transition-all"
                >
                  Subscribe
                </button>
              </form>
            </div>
          </div>

          <div className="border-t border-[#1A1A1A] pt-6 flex flex-col sm:flex-row items-center justify-between gap-4 text-[11px] text-[#B5B5B5]">
            <p>© {new Date().getFullYear()} {CONFIG.brandName} Fitness. Universal Website Demonstration. Built for athletic performance.</p>
            <div className="flex gap-4">
              <span className="hover:text-white cursor-pointer">Privacy Policy</span>
              <span className="hover:text-white cursor-pointer">Terms of Service</span>
              <span className="hover:text-white cursor-pointer" onClick={() => navigateTo("admin")}>Admin Panel</span>
            </div>
          </div>
        </div>
      </footer>

      {/* FLOATING WHATSAPP CTA */}
      <a
        href={`https://wa.me/${CONFIG.contact.whatsapp}?text=Hi,%20I%20would%20like%20to%20enquire%20about%20a%20gym%20membership!`}
        target="_blank"
        rel="noopener noreferrer"
        className="fixed bottom-6 right-6 z-40 bg-[#25D366] hover:bg-[#20ba5a] text-white p-3.5 rounded-full shadow-2xl transition-all duration-300 hover:scale-110 flex items-center justify-center border-2 border-white/20"
        title="Chat on WhatsApp"
      >
        <MessageCircle className="w-6 h-6 fill-current" />
      </a>

      {/* SCROLL TO TOP */}
      {showScrollTop && (
        <button
          onClick={() => window.scrollTo({ top: 0, behavior: "smooth" })}
          className="fixed bottom-6 left-6 z-40 bg-[#1A1A1A] hover:bg-[#FF303B] border border-white/10 text-white p-3 rounded-full shadow-xl transition-all duration-300 hover:scale-105"
        >
          <ChevronUp className="w-5 h-5" />
        </button>
      )}

      {/* LIGHTBOX MODAL */}
      {selectedImage && (
        <div className="fixed inset-0 z-50 bg-black/90 backdrop-blur-md flex items-center justify-center p-4">
          <div className="relative max-w-4xl w-full">
            <button
              onClick={() => setSelectedImage(null)}
              className="absolute -top-10 right-0 text-white hover:text-[#FF303B]"
            >
              <X className="w-8 h-8" />
            </button>
            <img
              src={selectedImage}
              alt="Facility Preview"
              className="w-full h-auto max-h-[80vh] object-contain rounded-xl border border-white/10"
            />
          </div>
        </div>
      )}

      {/* BOOKING & MEMBERSHIP MODAL */}
      {modalOpen && (
        <div className="fixed inset-0 z-50 bg-black/80 backdrop-blur-sm flex items-center justify-center p-4">
          <div className="bg-[#141414] border border-[#1A1A1A] rounded-2xl max-w-md w-full p-6 sm:p-8 relative shadow-2xl">
            <button
              onClick={() => setModalOpen(false)}
              className="absolute top-4 right-4 text-[#B5B5B5] hover:text-white"
            >
              <X className="w-6 h-6" />
            </button>

            {formSuccess ? (
              <div className="text-center py-8 space-y-4">
                <div className="w-16 h-16 bg-[#FF303B]/20 text-[#FF303B] rounded-full flex items-center justify-center mx-auto border border-[#FF303B]/40">
                  <CheckCircle2 className="w-10 h-10" />
                </div>
                <h3 className="text-2xl font-black uppercase text-white">Enquiry Submitted!</h3>
                <p className="text-xs text-[#B5B5B5]">
                  Thank you! Our fitness manager will contact you via WhatsApp/Phone shortly.
                </p>
              </div>
            ) : (
              <div>
                <div className="mb-6">
                  <span className="text-xs font-bold text-[#FF303B] tracking-widest uppercase">
                    {modalType === "trial" ? "VIP Day Pass Request" : "Membership Enquiry"}
                  </span>
                  <h3 className="text-2xl font-black text-white uppercase mt-1">
                    {modalType === "trial" ? "Book Free Trial Session" : "Join PULSE Fitness"}
                  </h3>
                  <p className="text-xs text-[#B5B5B5] mt-1">
                    Complete details below to secure demo membership rates.
                  </p>
                </div>

                <form onSubmit={handleFormSubmit} className="space-y-4">
                  <div>
                    <label className="block text-xs font-semibold uppercase tracking-wider text-[#B5B5B5] mb-1">
                      Full Name *
                    </label>
                    <input
                      type="text"
                      required
                      value={formData.name}
                      onChange={(e) => setFormData({ ...formData, name: e.target.value })}
                      placeholder="e.g. Rahul Sharma"
                      className="w-full bg-[#1A1A1A] border border-white/10 rounded-lg px-4 py-2.5 text-xs text-white focus:outline-none focus:border-[#FF303B]"
                    />
                  </div>

                  <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
                    <div>
                      <label className="block text-xs font-semibold uppercase tracking-wider text-[#B5B5B5] mb-1">
                        Phone Number *
                      </label>
                      <input
                        type="tel"
                        required
                        value={formData.phone}
                        onChange={(e) => setFormData({ ...formData, phone: e.target.value })}
                        placeholder="+91 98765 00000"
                        className="w-full bg-[#1A1A1A] border border-white/10 rounded-lg px-4 py-2.5 text-xs text-white focus:outline-none focus:border-[#FF303B]"
                      />
                    </div>
                    <div>
                      <label className="block text-xs font-semibold uppercase tracking-wider text-[#B5B5B5] mb-1">
                        Select Plan
                      </label>
                      <select
                        value={formData.plan}
                        onChange={(e) => setFormData({ ...formData, plan: e.target.value })}
                        className="w-full bg-[#1A1A1A] border border-white/10 rounded-lg px-3 py-2.5 text-xs text-white focus:outline-none focus:border-[#FF303B]"
                      >
                        <option value="Basic Plan">Basic Plan (₹999/mo)</option>
                        <option value="Pro Plan">Pro Plan (₹1,499/mo)</option>
                        <option value="Premium Plan">Premium Plan (₹1,999/mo)</option>
                      </select>
                    </div>
                  </div>

                  <div>
                    <label className="block text-xs font-semibold uppercase tracking-wider text-[#B5B5B5] mb-1">
                      Email Address
                    </label>
                    <input
                      type="email"
                      value={formData.email}
                      onChange={(e) => setFormData({ ...formData, email: e.target.value })}
                      placeholder="name@example.com"
                      className="w-full bg-[#1A1A1A] border border-white/10 rounded-lg px-4 py-2.5 text-xs text-white focus:outline-none focus:border-[#FF303B]"
                    />
                  </div>

                  <button
                    type="submit"
                    className="w-full bg-[#FF303B] hover:bg-[#e02630] text-white font-black py-3.5 rounded-lg text-xs uppercase tracking-wider transition-all shadow-lg shadow-[#FF303B]/30 mt-2"
                  >
                    Submit Booking Request
                  </button>
                </form>
              </div>
            )}
          </div>
        </div>
      )}
    </div>
  );
}

// ==========================================
// 1. HOME PAGE COMPONENT
// ==========================================
function HomePage({
  navigateTo,
  openBookingModal,
  setSelectedImage,
  billingCycle,
  setBillingCycle,
  calculatePrice,
  openFaq,
  setOpenFaq,
  scheduleData
}) {
  return (
    <div className="space-y-24 pb-20">
      
      {/* HERO SECTION */}
      <section className="relative min-h-[88vh] flex items-center justify-center overflow-hidden border-b border-[#1A1A1A]">
        <div className="absolute inset-0 z-0">
          <img
            src="https://images.unsplash.com/photo-1517838277536-f5f99be501cd?auto=format&fit=crop&q=80&w=1920"
            alt="Gym Hero Background"
            className="w-full h-full object-cover object-center opacity-30 scale-105"
          />
          <div className="absolute inset-0 bg-gradient-to-r from-[#080808] via-[#080808]/80 to-transparent"></div>
          <div className="absolute inset-0 bg-gradient-to-t from-[#080808] via-transparent to-transparent"></div>
        </div>

        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-20 relative z-10 grid grid-cols-1 lg:grid-cols-12 gap-12 items-center">
          
          <div className="lg:col-span-7 space-y-6 text-left">
            <div className="inline-flex items-center gap-2 bg-[#FF303B]/10 border border-[#FF303B]/30 px-3.5 py-1.5 rounded-full text-xs font-bold text-[#FF303B] tracking-wider uppercase">
              <Flame className="w-4 h-4" />
              <span>World-Class Athletic Infrastructure</span>
            </div>

            <h1 className="text-5xl sm:text-6xl xl:text-7xl font-black uppercase tracking-tight text-white leading-none">
              STRONGER <br />
              FITTER <br />
              <span className="text-[#FF303B]">HEALTHIER</span>
            </h1>

            <p className="text-[#B5B5B5] text-base sm:text-lg max-w-xl leading-relaxed">
              Transform your physique and endurance with professional coaching, heavy lifting racks, and metabolic conditioning zones.
            </p>

            <div className="flex flex-wrap items-center gap-4 pt-4">
              <button
                onClick={() => openBookingModal("join")}
                className="bg-[#FF303B] hover:bg-[#e02630] text-white font-black px-8 py-4 rounded-xl text-xs uppercase tracking-wider transition-all shadow-xl shadow-[#FF303B]/30 hover:shadow-[#FF303B]/50 hover:-translate-y-1 flex items-center gap-3"
              >
                <span>Join Membership</span>
                <ArrowRight className="w-4 h-4" />
              </button>

              <button
                onClick={() => openBookingModal("trial")}
                className="bg-[#1A1A1A] hover:bg-[#252525] border border-white/10 text-white font-bold px-7 py-4 rounded-xl text-xs uppercase tracking-wider transition-all hover:border-white/30 flex items-center gap-2"
              >
                <Play className="w-4 h-4 fill-current text-[#FF303B]" />
                <span>Explore VIP Pass</span>
              </button>
            </div>
          </div>

          <div className="lg:col-span-5 relative hidden lg:block">
            <div className="relative rounded-2xl overflow-hidden border border-white/10 shadow-2xl group">
              <img
                src="https://images.unsplash.com/photo-1583454110551-21f2fa2afe61?auto=format&fit=crop&q=80&w=800"
                alt="Athlete Training"
                className="w-full h-[460px] object-cover group-hover:scale-105 transition-transform duration-700"
              />
              <div className="absolute inset-0 bg-gradient-to-t from-[#080808] via-transparent to-transparent"></div>

              {/* Stat Widget */}
              <div className="absolute bottom-6 left-6 right-6 bg-[#141414]/90 backdrop-blur-md p-4 rounded-xl border border-white/10 shadow-xl space-y-3">
                <div className="flex items-center justify-between text-xs font-bold text-[#B5B5B5]">
                  <span>DAILY PERFORMANCE TRACKER</span>
                  <span className="text-[#FF303B]">88% COMPLETED</span>
                </div>
                <div className="w-full bg-[#1A1A1A] h-2 rounded-full overflow-hidden">
                  <div className="bg-[#FF303B] h-full w-[88%] rounded-full"></div>
                </div>
                <div className="grid grid-cols-3 gap-2 pt-1 text-center">
                  <div className="bg-[#1A1A1A] p-2 rounded-lg">
                    <span className="text-[10px] text-[#B5B5B5] block uppercase">Calories</span>
                    <span className="text-xs font-black text-white">650 kcal</span>
                  </div>
                  <div className="bg-[#1A1A1A] p-2 rounded-lg">
                    <span className="text-[10px] text-[#B5B5B5] block uppercase">Duration</span>
                    <span className="text-xs font-black text-white">55 mins</span>
                  </div>
                  <div className="bg-[#1A1A1A] p-2 rounded-lg">
                    <span className="text-[10px] text-[#B5B5B5] block uppercase">Intensity</span>
                    <span className="text-xs font-black text-[#FF303B]">High</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        {/* Dynamic Statistics Ribbon */}
        <div className="w-full bg-[#141414] border-t border-b border-[#1A1A1A] py-6">
          <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 grid grid-cols-2 md:grid-cols-4 gap-6">
            {STATS_DATA.map((stat, idx) => {
              const IconComp = stat.icon;
              return (
                <div key={idx} className="flex items-center gap-4 justify-center sm:justify-start">
                  <div className="w-12 h-12 bg-[#1A1A1A] border border-white/5 rounded-xl flex items-center justify-center shrink-0">
                    <IconComp className="w-6 h-6 text-[#FF303B]" />
                  </div>
                  <div>
                    <div className="text-2xl sm:text-3xl font-black text-white">{stat.value}</div>
                    <div className="text-[11px] text-[#B5B5B5] uppercase font-bold">{stat.label}</div>
                  </div>
                </div>
              );
            })}
          </div>
        </div>
      </section>

      {/* ABOUT OVERVIEW SECTION */}
      <section className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
          <div className="relative">
            <div className="rounded-2xl overflow-hidden border border-[#1A1A1A] shadow-2xl">
              <img
                src="https://images.unsplash.com/photo-1534438327276-14e5300c3a48?auto=format&fit=crop&q=80&w=800"
                alt="Gym Interior"
                className="w-full h-[400px] object-cover"
              />
            </div>
            <div className="absolute -bottom-6 -right-6 bg-[#FF303B] text-white p-6 rounded-2xl hidden sm:block shadow-xl max-w-[220px]">
              <span className="text-3xl font-black block">10+ YEARS</span>
              <span className="text-xs uppercase font-bold">Of Building Stronger Athletes & Body Transformations</span>
            </div>
          </div>

          <div className="space-y-6">
            <div>
              <span className="text-xs font-bold text-[#FF303B] uppercase tracking-widest block mb-1">
                ABOUT PULSE FITNESS
              </span>
              <h2 className="text-3xl sm:text-4xl font-black uppercase text-white">
                Your Fitness, <span className="text-[#FF303B]">Our Priority</span>
              </h2>
            </div>
            <p className="text-[#B5B5B5] text-sm leading-relaxed">
              We provide athletes and fitness enthusiasts with elite bio-mechanic strength machines, dedicated cardio suites, and custom nutritional guidance.
            </p>
            <div className="grid grid-cols-1 sm:grid-cols-2 gap-4 pt-2">
              {[
                "Certified Master Coaches",
                "Biomechanically Superior Racks",
                "Hygienic Hydrotherapy Sauna",
                "Customized Progress Tracking"
              ].map((item, idx) => (
                <div key={idx} className="flex items-center gap-2.5">
                  <CheckCircle2 className="w-4 h-4 text-[#FF303B] shrink-0" />
                  <span className="text-xs font-bold text-white uppercase">{item}</span>
                </div>
              ))}
            </div>
            <div className="pt-2">
              <button
                onClick={() => navigateTo("about")}
                className="bg-[#1A1A1A] hover:bg-[#FF303B] text-white font-bold px-6 py-3 rounded-lg text-xs uppercase tracking-wider transition-colors border border-white/10"
              >
                Learn More About Us
              </button>
            </div>
          </div>
        </div>
      </section>

      {/* FEATURED PROGRAMS PREVIEW */}
      <section className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="flex flex-col sm:flex-row items-start sm:items-end justify-between mb-12 gap-4">
          <div>
            <span className="text-xs font-bold text-[#FF303B] uppercase tracking-widest block mb-1">
              OUR PROGRAMS
            </span>
            <h2 className="text-3xl sm:text-4xl font-black uppercase text-white">
              Train <span className="text-[#FF303B]">Your Way</span>
            </h2>
          </div>
          <button
            onClick={() => navigateTo("programs")}
            className="text-xs text-[#FF303B] font-bold uppercase tracking-wider hover:underline flex items-center gap-1"
          >
            <span>View All Programs</span>
            <ChevronRight className="w-4 h-4" />
          </button>
        </div>

        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          {PROGRAMS_DATA.slice(0, 3).map((prog) => (
            <div
              key={prog.id}
              className="bg-[#141414] border border-[#1A1A1A] rounded-2xl overflow-hidden hover:border-[#FF303B]/50 transition-all duration-300 group flex flex-col"
            >
              <div className="relative h-48 overflow-hidden">
                <img
                  src={prog.image}
                  alt={prog.title}
                  className="w-full h-full object-cover group-hover:scale-110 transition-transform duration-500"
                />
                <div className="absolute inset-0 bg-gradient-to-t from-[#141414] via-transparent to-transparent"></div>
              </div>
              <div className="p-6 flex-1 flex flex-col justify-between space-y-4">
                <div>
                  <h3 className="text-lg font-bold uppercase text-white mb-2">{prog.title}</h3>
                  <p className="text-xs text-[#B5B5B5] leading-relaxed mb-4">{prog.desc}</p>
                  <ul className="space-y-1.5">
                    {prog.benefits.map((b, i) => (
                      <li key={i} className="text-[11px] text-white/80 flex items-center gap-2 font-medium">
                        <span className="w-1.5 h-1.5 rounded-full bg-[#FF303B]"></span>
                        <span>{b}</span>
                      </li>
                    ))}
                  </ul>
                </div>
                <button
                  onClick={() => openBookingModal("trial")}
                  className="w-full bg-[#1A1A1A] group-hover:bg-[#FF303B] text-white text-xs font-bold py-3 rounded-lg uppercase tracking-wider transition-colors flex items-center justify-center gap-2"
                >
                  <span>Explore Program</span>
                  <ArrowRight className="w-3.5 h-3.5" />
                </button>
              </div>
            </div>
          ))}
        </div>
      </section>

      {/* MEMBERSHIP PRICING CARDS */}
      <section className="bg-[#141414] py-20 border-t border-b border-[#1A1A1A]">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="text-center max-w-2xl mx-auto mb-12 space-y-3">
            <span className="text-xs font-bold text-[#FF303B] uppercase tracking-widest block">
              MEMBERSHIP PLANS
            </span>
            <h2 className="text-3xl sm:text-4xl font-black uppercase text-white">
              Find The <span className="text-[#FF303B]">Right Plan</span>
            </h2>
            <p className="text-xs text-[#B5B5B5]">
              Flexible membership packages designed for every commitment level and fitness objective.
            </p>

            <div className="inline-flex bg-[#1A1A1A] p-1.5 rounded-xl border border-white/10 mt-4">
              {["monthly", "quarterly", "yearly"].map((cycle) => (
                <button
                  key={cycle}
                  onClick={() => setBillingCycle(cycle)}
                  className={`px-4 py-2 rounded-lg text-[11px] font-bold uppercase tracking-wider transition-all ${
                    billingCycle === cycle ? "bg-[#FF303B] text-white shadow" : "text-[#B5B5B5] hover:text-white"
                  }`}
                >
                  {cycle === "monthly" ? "Monthly" : cycle === "quarterly" ? "Quarterly (-10%)" : "Yearly (-20%)"}
                </button>
              ))}
            </div>
          </div>

          <div className="grid grid-cols-1 md:grid-cols-3 gap-8 items-stretch">
            {MEMBERSHIP_PLANS.map((plan, idx) => {
              const finalPrice = calculatePrice(plan.monthlyPrice);
              return (
                <div
                  key={idx}
                  className={`relative bg-[#1A1A1A] rounded-2xl p-8 flex flex-col justify-between border transition-all duration-300 ${
                    plan.isPopular
                      ? "border-[#FF303B] shadow-2xl shadow-[#FF303B]/10 scale-105 z-10"
                      : "border-white/5 hover:border-white/20"
                  }`}
                >
                  {plan.isPopular && (
                    <div className="absolute -top-3.5 left-1/2 -translate-x-1/2 bg-[#FF303B] text-white text-[10px] font-black uppercase tracking-widest px-4 py-1 rounded-full shadow-md">
                      Most Popular Plan
                    </div>
                  )}

                  <div>
                    <h3 className="text-xl font-bold uppercase text-white mb-1">{plan.name}</h3>
                    <p className="text-xs text-[#B5B5B5] mb-6">{plan.desc}</p>

                    <div className="mb-6 border-b border-white/10 pb-6">
                      <span className="text-4xl font-black text-white">₹{finalPrice}</span>
                      <span className="text-xs text-[#B5B5B5] uppercase font-semibold"> / month</span>
                    </div>

                    <ul className="space-y-3 mb-8">
                      {plan.features.map((feat, fIdx) => (
                        <li key={fIdx} className="flex items-start gap-3 text-xs text-[#B5B5B5]">
                          <CheckCircle2 className="w-4 h-4 text-[#FF303B] shrink-0 mt-0.5" />
                          <span>{feat}</span>
                        </li>
                      ))}
                    </ul>
                  </div>

                  <button
                    onClick={() => openBookingModal("join")}
                    className={`w-full py-3.5 rounded-xl font-bold text-xs uppercase tracking-wider transition-all flex items-center justify-center gap-2 ${
                      plan.isPopular
                        ? "bg-[#FF303B] hover:bg-[#e02630] text-white shadow-lg shadow-[#FF303B]/30"
                        : "bg-[#141414] hover:bg-white hover:text-black text-white border border-white/10"
                    }`}
                  >
                    <span>Get Started</span>
                    <ArrowRight className="w-4 h-4" />
                  </button>
                </div>
              );
            })}
          </div>
        </div>
      </section>

      {/* SCHEDULE PREVIEW SECTION */}
      <section className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="flex flex-col sm:flex-row items-start sm:items-end justify-between mb-8 gap-4">
          <div>
            <span className="text-xs font-bold text-[#FF303B] uppercase tracking-widest block mb-1">
              CLASS TIMETABLE
            </span>
            <h2 className="text-3xl sm:text-4xl font-black uppercase text-white">
              Workout <span className="text-[#FF303B]">Schedule</span>
            </h2>
          </div>
          <button
            onClick={() => navigateTo("schedule")}
            className="text-xs text-[#FF303B] font-bold uppercase tracking-wider hover:underline flex items-center gap-1"
          >
            <span>View Full Schedule</span>
            <ChevronRight className="w-4 h-4" />
          </button>
        </div>

        <div className="bg-[#141414] border border-[#1A1A1A] rounded-2xl p-4 overflow-x-auto">
          <table className="w-full text-center text-xs">
            <thead>
              <tr className="bg-[#1A1A1A] text-white font-bold uppercase border-b border-white/10">
                <th className="py-3 px-3 text-left">Time</th>
                <th className="py-3 px-3">Mon</th>
                <th className="py-3 px-3">Tue</th>
                <th className="py-3 px-3">Wed</th>
                <th className="py-3 px-3">Thu</th>
                <th className="py-3 px-3">Fri</th>
                <th className="py-3 px-3 text-[#FF303B]">Sat</th>
                <th className="py-3 px-3 text-[#B5B5B5]">Sun</th>
              </tr>
            </thead>
            <tbody className="divide-y divide-white/5 text-[#B5B5B5]">
              {scheduleData.map((row, idx) => (
                <tr key={idx} className="hover:bg-[#1A1A1A]/50">
                  <td className="py-3.5 px-3 font-semibold text-left text-white whitespace-nowrap">{row.time}</td>
                  <td className="py-3.5 px-3"><span className="bg-[#1A1A1A] px-2.5 py-1 rounded text-white font-medium">{row.mon}</span></td>
                  <td className="py-3.5 px-3"><span className="bg-[#1A1A1A] px-2.5 py-1 rounded text-white font-medium">{row.tue}</span></td>
                  <td className="py-3.5 px-3"><span className="bg-[#1A1A1A] px-2.5 py-1 rounded text-white font-medium">{row.wed}</span></td>
                  <td className="py-3.5 px-3"><span className="bg-[#1A1A1A] px-2.5 py-1 rounded text-white font-medium">{row.thu}</span></td>
                  <td className="py-3.5 px-3"><span className="bg-[#1A1A1A] px-2.5 py-1 rounded text-white font-medium">{row.fri}</span></td>
                  <td className="py-3.5 px-3"><span className="bg-[#FF303B]/20 text-[#FF303B] px-2.5 py-1 rounded font-bold">{row.sat}</span></td>
                  <td className="py-3.5 px-3"><span className="text-white/40">{row.sun}</span></td>
                </tr>
              ))}
            </tbody>
          </table>
        </div>
      </section>

      {/* FAQ SECTION */}
      <section className="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="text-center mb-10">
          <span className="text-xs font-bold text-[#FF303B] uppercase tracking-widest block mb-1">
            QUESTIONS & ANSWERS
          </span>
          <h2 className="text-3xl font-black uppercase text-white">Frequently Asked Questions</h2>
        </div>

        <div className="space-y-4">
          {FAQS_DATA.map((faq, idx) => (
            <div key={idx} className="bg-[#141414] border border-[#1A1A1A] rounded-xl overflow-hidden">
              <button
                onClick={() => setOpenFaq(openFaq === idx ? null : idx)}
                className="w-full px-6 py-4 text-left flex items-center justify-between font-bold text-white text-xs uppercase tracking-wider hover:text-[#FF303B] transition-colors"
              >
                <span>{faq.q}</span>
                <ChevronRight
                  className={`w-4 h-4 text-[#FF303B] transition-transform ${
                    openFaq === idx ? "rotate-90" : ""
                  }`}
                />
              </button>
              {openFaq === idx && (
                <div className="px-6 pb-4 text-xs text-[#B5B5B5] leading-relaxed border-t border-white/5 pt-3">
                  {faq.a}
                </div>
              )}
            </div>
          ))}
        </div>
      </section>

      {/* FINAL CTA BANNER */}
      <section className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="relative rounded-3xl overflow-hidden bg-gradient-to-r from-[#FF303B] to-[#99000a] p-10 sm:p-14 text-center sm:text-left flex flex-col sm:flex-row items-center justify-between gap-8 shadow-2xl">
          <div className="space-y-2 max-w-xl">
            <h2 className="text-3xl sm:text-4xl font-black uppercase text-white">
              Ready To Begin Your Transformation?
            </h2>
            <p className="text-white/80 text-xs">
              Claim your 1-day complimentary VIP pass today and experience our gym floor firsthand.
            </p>
          </div>
          <button
            onClick={() => openBookingModal("trial")}
            className="bg-black hover:bg-neutral-900 text-white font-black px-8 py-4 rounded-xl text-xs uppercase tracking-wider transition-all shadow-xl shrink-0"
          >
            Claim VIP Pass Now
          </button>
        </div>
      </section>
    </div>
  );
}

// ==========================================
// 2. ABOUT PAGE COMPONENT
// ==========================================
function AboutPage({ openBookingModal }) {
  return (
    <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 space-y-16">
      <div className="text-center max-w-3xl mx-auto space-y-4">
        <span className="text-xs font-bold text-[#FF303B] uppercase tracking-widest block">
          OUR PHILOSOPHY & VISION
        </span>
        <h1 className="text-4xl sm:text-5xl font-black uppercase text-white">
          More Than A Gym — <span className="text-[#FF303B]">A Lifestyle</span>
        </h1>
        <p className="text-[#B5B5B5] text-sm leading-relaxed">
          Founded on principles of raw athletic progression, biomechanical precision, and supportive community, PULSE provides state-of-the-art infrastructure for every step of your fitness journey.
        </p>
      </div>

      <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
        {[
          { title: "Our Mission", desc: "To inspire and empower individuals to live healthier, stronger, and more confident lives through disciplined athletic training." },
          { title: "Our Vision", desc: "To build a world-class fitness community driven by athletic excellence, high-performance coaching, and genuine support." },
          { title: "Our Core Values", desc: "Consistency, progressive overload, bio-individual meal planning, and continuous physical self-improvement." }
        ].map((card, idx) => (
          <div key={idx} className="bg-[#141414] border border-[#1A1A1A] p-8 rounded-2xl text-center space-y-3">
            <div className="w-12 h-12 bg-[#FF303B]/10 rounded-full flex items-center justify-center mx-auto text-[#FF303B]">
              <Trophy className="w-6 h-6" />
            </div>
            <h3 className="text-lg font-bold uppercase text-white">{card.title}</h3>
            <p className="text-xs text-[#B5B5B5] leading-relaxed">{card.desc}</p>
          </div>
        ))}
      </div>

      <div className="bg-[#141414] border border-[#1A1A1A] rounded-2xl p-8 sm:p-12 grid grid-cols-1 lg:grid-cols-2 gap-8 items-center">
        <div className="space-y-4">
          <h2 className="text-3xl font-black uppercase text-white">Why Choose Our Facility?</h2>
          <ul className="space-y-3">
            {[
              "High-grade imported biomechanical strength machinery",
              "Certified strength & conditioning master coaches on floor",
              "Spacious dedicated synthetic turf zones for functional drills",
              "Clean, climate-controlled environments with saunas",
              "Nutritional support & body composition analysis"
            ].map((point, i) => (
              <li key={i} className="flex items-center gap-3 text-xs text-[#B5B5B5]">
                <CheckCircle2 className="w-4 h-4 text-[#FF303B] shrink-0" />
                <span>{point}</span>
              </li>
            ))}
          </ul>
          <div className="pt-4">
            <button
              onClick={() => openBookingModal("trial")}
              className="bg-[#FF303B] hover:bg-[#e02630] text-white font-bold px-6 py-3 rounded-lg text-xs uppercase tracking-wider"
            >
              Book Free Orientation
            </button>
          </div>
        </div>
        <div>
          <img
            src="https://images.unsplash.com/photo-1540555700478-4be289fbecef?auto=format&fit=crop&q=80&w=800"
            alt="Gym Atmosphere"
            className="rounded-xl border border-white/10 shadow-lg object-cover w-full h-80"
          />
        </div>
      </div>
    </div>
  );
}

// ==========================================
// 3. PROGRAMS PAGE COMPONENT
// ==========================================
function ProgramsPage({ openBookingModal }) {
  const [filter, setFilter] = useState("all");

  const filteredPrograms = filter === "all" ? PROGRAMS_DATA : PROGRAMS_DATA.filter((p) => p.category === filter);

  return (
    <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 space-y-12">
      <div className="text-center max-w-3xl mx-auto space-y-3">
        <span className="text-xs font-bold text-[#FF303B] uppercase tracking-widest block">
          WORKOUT BLUEPRINTS
        </span>
        <h1 className="text-4xl sm:text-5xl font-black uppercase text-white">
          Explore Our <span className="text-[#FF303B]">Programs</span>
        </h1>
        <p className="text-[#B5B5B5] text-xs">
          Filter programs based on your athletic goals: strength hypertrophy, cardio fat loss, functional agility, or postural mobility.
        </p>

        <div className="flex flex-wrap items-center justify-center gap-2 pt-4">
          {[
            { id: "all", label: "All Programs" },
            { id: "strength", label: "Strength & Muscle" },
            { id: "cardio", label: "Cardio & HIIT" },
            { id: "functional", label: "Functional" },
            { id: "mobility", label: "Mobility & Yoga" }
          ].map((tab) => (
            <button
              key={tab.id}
              onClick={() => setFilter(tab.id)}
              className={`px-4 py-2 rounded-lg text-xs font-bold uppercase tracking-wider transition-all ${
                filter === tab.id
                  ? "bg-[#FF303B] text-white"
                  : "bg-[#141414] text-[#B5B5B5] border border-[#1A1A1A] hover:text-white"
              }`}
            >
              {tab.label}
            </button>
          ))}
        </div>
      </div>

      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        {filteredPrograms.map((prog) => (
          <div
            key={prog.id}
            className="bg-[#141414] border border-[#1A1A1A] rounded-2xl overflow-hidden hover:border-[#FF303B]/40 transition-all flex flex-col justify-between"
          >
            <div>
              <div className="relative">
                <img src={prog.image} alt={prog.title} className="w-full h-52 object-cover" />
                <span className="absolute top-3 right-3 bg-black/80 backdrop-blur-md text-[#FF303B] border border-[#FF303B]/30 px-3 py-1 rounded-full text-[10px] font-bold uppercase tracking-widest">
                  {prog.intensity} Intensity
                </span>
              </div>
              <div className="p-6 space-y-3">
                <h3 className="text-lg font-bold uppercase text-white">{prog.title}</h3>
                <p className="text-xs text-[#B5B5B5] leading-relaxed">{prog.desc}</p>
                <div className="space-y-2 pt-2">
                  <span className="text-[10px] font-bold uppercase text-[#FF303B] tracking-wider block">
                    Core Benefits:
                  </span>
                  {prog.benefits.map((b, i) => (
                    <div key={i} className="flex items-center gap-2 text-xs text-[#B5B5B5]">
                      <CheckCircle2 className="w-3.5 h-3.5 text-[#FF303B]" />
                      <span>{b}</span>
                    </div>
                  ))}
                </div>
              </div>
            </div>
            <div className="p-6 pt-0">
              <button
                onClick={() => openBookingModal("trial")}
                className="w-full bg-[#1A1A1A] hover:bg-[#FF303B] text-white font-bold py-3 rounded-lg text-xs uppercase tracking-wider transition-colors"
              >
                Book Program Trial
              </button>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
}

// ==========================================
// 4. TRAINERS PAGE COMPONENT
// ==========================================
function TrainersPage({ openBookingModal }) {
  return (
    <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 space-y-12">
      <div className="text-center max-w-3xl mx-auto space-y-3">
        <span className="text-xs font-bold text-[#FF303B] uppercase tracking-widest block">
          MASTER COACHES
        </span>
        <h1 className="text-4xl sm:text-5xl font-black uppercase text-white">
          Learn From <span className="text-[#FF303B]">The Best</span>
        </h1>
        <p className="text-[#B5B5B5] text-xs">
          Our master trainers hold international strength & conditioning certifications and are dedicated to your athletic success.
        </p>
      </div>

      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
        {TRAINERS_DATA.map((trainer) => (
          <div
            key={trainer.id}
            className="bg-[#141414] border border-[#1A1A1A] rounded-2xl overflow-hidden hover:border-[#FF303B]/50 transition-all flex flex-col justify-between"
          >
            <div>
              <img src={trainer.image} alt={trainer.name} className="w-full h-72 object-cover object-top" />
              <div className="p-6 space-y-3">
                <div>
                  <h3 className="text-lg font-bold uppercase text-white">{trainer.name}</h3>
                  <span className="text-xs font-semibold text-[#FF303B] uppercase">{trainer.role}</span>
                </div>
                <div className="text-[10px] bg-[#1A1A1A] px-2.5 py-1 rounded text-[#B5B5B5] inline-block font-mono">
                  {trainer.exp}
                </div>
                <p className="text-xs text-[#B5B5B5] leading-relaxed">{trainer.bio}</p>
              </div>
            </div>

            <div className="p-6 pt-0">
              <button
                onClick={() => openBookingModal("trial")}
                className="w-full bg-[#1A1A1A] hover:bg-[#FF303B] text-white font-bold py-2.5 rounded-lg text-xs uppercase tracking-wider transition-colors"
              >
                Book Personal Session
              </button>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
}

// ==========================================
// 5. MEMBERSHIP PAGE COMPONENT
// ==========================================
function MembershipPage({
  billingCycle,
  setBillingCycle,
  calculatePrice,
  openBookingModal,
  openFaq,
  setOpenFaq
}) {
  return (
    <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 space-y-16">
      <div className="text-center max-w-3xl mx-auto space-y-4">
        <span className="text-xs font-bold text-[#FF303B] uppercase tracking-widest block">
          PRICING & PACKAGES
        </span>
        <h1 className="text-4xl sm:text-5xl font-black uppercase text-white">
          Choose The <span className="text-[#FF303B]">Perfect Plan</span>
        </h1>
        <p className="text-[#B5B5B5] text-xs">
          Transparent pricing structure. Zero initiation hidden charges. Select your commitment billing cycle.
        </p>

        <div className="inline-flex bg-[#141414] p-1.5 rounded-xl border border-[#1A1A1A] mt-4">
          {["monthly", "quarterly", "yearly"].map((cycle) => (
            <button
              key={cycle}
              onClick={() => setBillingCycle(cycle)}
              className={`px-5 py-2.5 rounded-lg text-xs font-bold uppercase tracking-wider transition-all ${
                billingCycle === cycle ? "bg-[#FF303B] text-white shadow-lg" : "text-[#B5B5B5] hover:text-white"
              }`}
            >
              {cycle === "monthly" ? "Monthly" : cycle === "quarterly" ? "Quarterly (-10%)" : "Yearly (-20%)"}
            </button>
          ))}
        </div>
      </div>

      <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
        {MEMBERSHIP_PLANS.map((plan, idx) => {
          const finalPrice = calculatePrice(plan.monthlyPrice);
          return (
            <div
              key={idx}
              className={`bg-[#141414] rounded-2xl p-8 border flex flex-col justify-between ${
                plan.isPopular ? "border-[#FF303B] shadow-2xl relative" : "border-[#1A1A1A]"
              }`}
            >
              {plan.isPopular && (
                <span className="absolute -top-3.5 left-1/2 -translate-x-1/2 bg-[#FF303B] text-white text-[10px] font-black uppercase px-4 py-1 rounded-full">
                  Recommended Choice
                </span>
              )}
              <div>
                <h3 className="text-xl font-bold uppercase text-white mb-2">{plan.name}</h3>
                <p className="text-xs text-[#B5B5B5] mb-6">{plan.desc}</p>
                <div className="mb-6 pb-6 border-b border-white/5">
                  <span className="text-4xl font-black text-white">₹{finalPrice}</span>
                  <span className="text-xs text-[#B5B5B5] uppercase"> / month</span>
                </div>
                <ul className="space-y-3 mb-8">
                  {plan.features.map((feat, fIdx) => (
                    <li key={fIdx} className="flex items-center gap-3 text-xs text-[#B5B5B5]">
                      <CheckCircle2 className="w-4 h-4 text-[#FF303B] shrink-0" />
                      <span>{feat}</span>
                    </li>
                  ))}
                </ul>
              </div>
              <button
                onClick={() => openBookingModal("join")}
                className={`w-full py-3.5 rounded-xl font-bold text-xs uppercase tracking-wider transition-all ${
                  plan.isPopular ? "bg-[#FF303B] text-white shadow-lg" : "bg-[#1A1A1A] hover:bg-white hover:text-black text-white"
                }`}
              >
                Join Now
              </button>
            </div>
          );
        })}
      </div>

      {/* Feature Comparison Table */}
      <div className="bg-[#141414] border border-[#1A1A1A] rounded-2xl p-6 sm:p-8 overflow-x-auto">
        <h3 className="text-xl font-bold uppercase text-white mb-6">Full Feature Comparison Matrix</h3>
        <table className="w-full text-left text-xs border-collapse">
          <thead>
            <tr className="border-b border-white/10 text-[#B5B5B5] uppercase">
              <th className="py-3 px-4 font-bold">Privilege / Feature</th>
              <th className="py-3 px-4 font-bold">Basic Plan</th>
              <th className="py-3 px-4 font-bold text-[#FF303B]">Pro Plan</th>
              <th className="py-3 px-4 font-bold">Premium Plan</th>
            </tr>
          </thead>
          <tbody className="divide-y divide-white/5 text-[#B5B5B5]">
            {[
              { f: "24/7 Floor Access", b: "No", p: "Yes", pr: "Yes" },
              { f: "Standard Locker Access", b: "Yes", p: "Yes", pr: "Dedicated Permanent Locker" },
              { f: "Sauna & Steam Bath", b: "No", p: "Yes", pr: "Unlimited" },
              { f: "Personal Master Coach", b: "None", p: "2 Sessions/Mo", pr: "Unlimited Dedicated" },
              { f: "Nutrition & Macro Blueprint", b: "Basic Overview", p: "Custom Plan", pr: "Full Bio-Individual Protocol" },
              { f: "Guest Passes", b: "0", p: "1 / month", pr: "3 / month" }
            ].map((row, idx) => (
              <tr key={idx} className="hover:bg-[#1A1A1A]">
                <td className="py-3.5 px-4 font-semibold text-white">{row.f}</td>
                <td className="py-3.5 px-4">{row.b}</td>
                <td className="py-3.5 px-4 text-white font-medium">{row.p}</td>
                <td className="py-3.5 px-4 text-[#FF303B] font-bold">{row.pr}</td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
    </div>
  );
}

// ==========================================
// 6. GALLERY & FACILITIES PAGE COMPONENT
// ==========================================
function GalleryPage({ setSelectedImage }) {
  const [category, setCategory] = useState("all");

  const filteredImages = category === "all" ? GALLERY_IMAGES : GALLERY_IMAGES.filter((g) => g.category === category);

  return (
    <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 space-y-12">
      <div className="text-center max-w-3xl mx-auto space-y-3">
        <span className="text-xs font-bold text-[#FF303B] uppercase tracking-widest block">
          FACILITIES SHOWCASE
        </span>
        <h1 className="text-4xl sm:text-5xl font-black uppercase text-white">
          Gym & Infrastructure <span className="text-[#FF303B]">Gallery</span>
        </h1>
        <p className="text-[#B5B5B5] text-xs">
          Click any image to open full-screen high-resolution lightbox view.
        </p>

        <div className="flex flex-wrap items-center justify-center gap-2 pt-4">
          {[
            { id: "all", label: "All Facilities" },
            { id: "strength", label: "Strength Floor" },
            { id: "cardio", label: "Cardio Arena" },
            { id: "functional", label: "Functional Turf" },
            { id: "facilities", label: "Sauna & Amenities" }
          ].map((cat) => (
            <button
              key={cat.id}
              onClick={() => setCategory(cat.id)}
              className={`px-4 py-2 rounded-lg text-xs font-bold uppercase tracking-wider transition-all ${
                category === cat.id
                  ? "bg-[#FF303B] text-white"
                  : "bg-[#141414] text-[#B5B5B5] border border-[#1A1A1A] hover:text-white"
              }`}
            >
              {cat.label}
            </button>
          ))}
        </div>
      </div>

      <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
        {filteredImages.map((img) => (
          <div
            key={img.id}
            onClick={() => setSelectedImage(img.src)}
            className="group relative h-64 rounded-2xl overflow-hidden cursor-pointer border border-[#1A1A1A] hover:border-[#FF303B]/60 transition-all"
          >
            <img
              src={img.src}
              alt={img.title}
              className="w-full h-full object-cover group-hover:scale-110 transition-transform duration-500"
            />
            <div className="absolute inset-0 bg-gradient-to-t from-black/80 via-black/20 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex flex-col justify-end p-6">
              <span className="text-sm font-bold text-white uppercase">{img.title}</span>
              <span className="text-xs text-[#FF303B] font-semibold flex items-center gap-1 mt-1">
                <Maximize2 className="w-3.5 h-3.5" /> Enlarge View
              </span>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
}

// ==========================================
// 7. CLASS SCHEDULE PAGE COMPONENT
// ==========================================
function SchedulePage({ scheduleData, openBookingModal }) {
  return (
    <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 space-y-12">
      <div className="text-center max-w-3xl mx-auto space-y-3">
        <span className="text-xs font-bold text-[#FF303B] uppercase tracking-widest block">
          FULL WEEKLY TIMETABLE
        </span>
        <h1 className="text-4xl sm:text-5xl font-black uppercase text-white">
          Group Class <span className="text-[#FF303B]">Schedule</span>
        </h1>
        <p className="text-[#B5B5B5] text-xs">
          Reserve your slot in advance for small-group functional and strength sessions.
        </p>
      </div>

      <div className="bg-[#141414] border border-[#1A1A1A] rounded-2xl p-4 sm:p-6 overflow-x-auto shadow-2xl">
        <table className="w-full text-center text-xs border-collapse">
          <thead>
            <tr className="bg-[#1A1A1A] text-white font-bold uppercase border-b border-white/10">
              <th className="py-4 px-3 text-left">Time Slot</th>
              <th className="py-4 px-3">Monday</th>
              <th className="py-4 px-3">Tuesday</th>
              <th className="py-4 px-3">Wednesday</th>
              <th className="py-4 px-3">Thursday</th>
              <th className="py-4 px-3">Friday</th>
              <th className="py-4 px-3 text-[#FF303B]">Saturday</th>
              <th className="py-4 px-3 text-[#B5B5B5]">Sunday</th>
            </tr>
          </thead>
          <tbody className="divide-y divide-white/5 text-[#B5B5B5]">
            {scheduleData.map((row, idx) => (
              <tr key={idx} className="hover:bg-[#1A1A1A]/60">
                <td className="py-4 px-3 font-semibold text-left text-white whitespace-nowrap">{row.time}</td>
                <td className="py-4 px-3"><span className="bg-[#1A1A1A] px-2.5 py-1 rounded text-white font-medium">{row.mon}</span></td>
                <td className="py-4 px-3"><span className="bg-[#1A1A1A] px-2.5 py-1 rounded text-white font-medium">{row.tue}</span></td>
                <td className="py-4 px-3"><span className="bg-[#1A1A1A] px-2.5 py-1 rounded text-white font-medium">{row.wed}</span></td>
                <td className="py-4 px-3"><span className="bg-[#1A1A1A] px-2.5 py-1 rounded text-white font-medium">{row.thu}</span></td>
                <td className="py-4 px-3"><span className="bg-[#1A1A1A] px-2.5 py-1 rounded text-white font-medium">{row.fri}</span></td>
                <td className="py-4 px-3"><span className="bg-[#FF303B]/20 text-[#FF303B] px-2.5 py-1 rounded font-bold">{row.sat}</span></td>
                <td className="py-4 px-3"><span className="text-white/40">{row.sun}</span></td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>

      <div className="text-center">
        <button
          onClick={() => openBookingModal("trial")}
          className="bg-[#FF303B] hover:bg-[#e02630] text-white font-bold px-8 py-3.5 rounded-xl text-xs uppercase tracking-wider shadow-lg shadow-[#FF303B]/30"
        >
          Book Class Reservation
        </button>
      </div>
    </div>
  );
}

// ==========================================
// 8. REVIEWS PAGE COMPONENT
// ==========================================
function ReviewsPage({ openBookingModal }) {
  return (
    <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 space-y-12">
      <div className="text-center max-w-3xl mx-auto space-y-3">
        <span className="text-xs font-bold text-[#FF303B] uppercase tracking-widest block">
          ATHLETE REVIEWS
        </span>
        <h1 className="text-4xl sm:text-5xl font-black uppercase text-white">
          Client <span className="text-[#FF303B]">Testimonials</span>
        </h1>
        <p className="text-[#B5B5B5] text-xs">
          Read genuine experiences from members who transformed their health and conditioning at PULSE.
        </p>
      </div>

      <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
        {REVIEWS_DATA.map((rev, idx) => (
          <div key={idx} className="bg-[#141414] border border-[#1A1A1A] p-6 rounded-2xl space-y-4 flex flex-col justify-between">
            <div className="space-y-3">
              <div className="flex gap-1 text-[#FF303B]">
                {[...Array(rev.rating)].map((_, i) => (
                  <Star key={i} className="w-4 h-4 fill-current" />
                ))}
              </div>
              <p className="text-xs text-[#B5B5B5] leading-relaxed italic">"{rev.comment}"</p>
            </div>
            <div className="border-t border-white/5 pt-3">
              <h4 className="text-sm font-bold uppercase text-white">{rev.name}</h4>
              <span className="text-[11px] text-[#FF303B] font-medium">{rev.role}</span>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
}

// ==========================================
// 9. CONTACT PAGE COMPONENT
// ==========================================
function ContactPage() {
  const [submitted, setSubmitted] = useState(false);

  const handleSubmit = (e) => {
    e.preventDefault();
    setSubmitted(true);
  };

  return (
    <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 space-y-12">
      <div className="text-center max-w-3xl mx-auto space-y-3">
        <span className="text-xs font-bold text-[#FF303B] uppercase tracking-widest block">
          GET IN TOUCH
        </span>
        <h1 className="text-4xl sm:text-5xl font-black uppercase text-white">
          Contact <span className="text-[#FF303B]">Us</span>
        </h1>
        <p className="text-[#B5B5B5] text-xs">Have questions about memberships or personal coaching? Send a message to our desk.</p>
      </div>

      <div className="grid grid-cols-1 lg:grid-cols-12 gap-12 items-start">
        <div className="lg:col-span-5 space-y-6">
          <div className="bg-[#141414] border border-[#1A1A1A] p-6 rounded-2xl flex items-start gap-4">
            <div className="w-10 h-10 bg-[#FF303B]/10 text-[#FF303B] rounded-xl flex items-center justify-center shrink-0">
              <MapPin className="w-5 h-5" />
            </div>
            <div>
              <h4 className="text-sm font-bold uppercase text-white mb-1">Gym Location</h4>
              <p className="text-xs text-[#B5B5B5] leading-relaxed">{CONFIG.contact.address}</p>
            </div>
          </div>

          <div className="bg-[#141414] border border-[#1A1A1A] p-6 rounded-2xl flex items-start gap-4">
            <div className="w-10 h-10 bg-[#FF303B]/10 text-[#FF303B] rounded-xl flex items-center justify-center shrink-0">
              <Phone className="w-5 h-5" />
            </div>
            <div>
              <h4 className="text-sm font-bold uppercase text-white mb-1">Phone & WhatsApp</h4>
              <p className="text-xs text-[#B5B5B5]">{CONFIG.contact.phone}</p>
            </div>
          </div>

          <div className="bg-[#141414] border border-[#1A1A1A] p-6 rounded-2xl flex items-start gap-4">
            <div className="w-10 h-10 bg-[#FF303B]/10 text-[#FF303B] rounded-xl flex items-center justify-center shrink-0">
              <Mail className="w-5 h-5" />
            </div>
            <div>
              <h4 className="text-sm font-bold uppercase text-white mb-1">Email Enquiry</h4>
              <p className="text-xs text-[#B5B5B5]">{CONFIG.contact.email}</p>
            </div>
          </div>
        </div>

        <div className="lg:col-span-7 bg-[#141414] border border-[#1A1A1A] p-8 rounded-2xl">
          {submitted ? (
            <div className="text-center py-12 space-y-3">
              <CheckCircle2 className="w-12 h-12 text-[#FF303B] mx-auto" />
              <h3 className="text-2xl font-black uppercase text-white">Message Sent!</h3>
              <p className="text-xs text-[#B5B5B5]">We will get back to you shortly via phone/email.</p>
            </div>
          ) : (
            <form onSubmit={handleSubmit} className="space-y-4">
              <h3 className="text-xl font-black uppercase text-white mb-4">Send A Direct Message</h3>
              <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
                <input
                  type="text"
                  required
                  placeholder="Your Name"
                  className="bg-[#1A1A1A] border border-white/10 rounded-lg px-4 py-3 text-xs text-white focus:outline-none focus:border-[#FF303B]"
                />
                <input
                  type="email"
                  required
                  placeholder="Your Email"
                  className="bg-[#1A1A1A] border border-white/10 rounded-lg px-4 py-3 text-xs text-white focus:outline-none focus:border-[#FF303B]"
                />
              </div>
              <input
                type="tel"
                required
                placeholder="Phone Number"
                className="w-full bg-[#1A1A1A] border border-white/10 rounded-lg px-4 py-3 text-xs text-white focus:outline-none focus:border-[#FF303B]"
              />
              <textarea
                rows={4}
                required
                placeholder="Your Message / Query"
                className="w-full bg-[#1A1A1A] border border-white/10 rounded-lg px-4 py-3 text-xs text-white focus:outline-none focus:border-[#FF303B]"
              ></textarea>
              <button
                type="submit"
                className="w-full bg-[#FF303B] hover:bg-[#e02630] text-white font-bold py-3.5 rounded-lg text-xs uppercase tracking-wider shadow-lg"
              >
                Send Message
              </button>
            </form>
          )}
        </div>
      </div>
    </div>
  );
}

// ==========================================
// 10. DEMO ADMIN DASHBOARD COMPONENT
// ==========================================
function AdminDashboard({ enquiries, setEnquiries, scheduleData, setScheduleData }) {
  const [activeTab, setActiveTab] = useState("enquiries");
  const [newSlotTime, setNewSlotTime] = useState("");
  const [newSlotClass, setNewSlotClass] = useState("Strength");

  const addScheduleRow = () => {
    if (!newSlotTime) return;
    setScheduleData([
      ...scheduleData,
      {
        time: newSlotTime,
        mon: newSlotClass,
        tue: newSlotClass,
        wed: newSlotClass,
        thu: newSlotClass,
        fri: newSlotClass,
        sat: newSlotClass,
        sun: "Rest"
      }
    ]);
    setNewSlotTime("");
  };

  return (
    <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-10 space-y-8">
      
      {/* Prototype Warning Banner */}
      <div className="bg-[#141414] border border-[#FF303B]/40 rounded-xl p-4 flex flex-col sm:flex-row items-center justify-between gap-4">
        <div className="flex items-center gap-3">
          <div className="w-3 h-3 rounded-full bg-[#FF303B] animate-pulse"></div>
          <div>
            <span className="text-xs font-bold text-white uppercase tracking-wider block">
              DEMO ADMIN PROTOTYPE ACTIVE
            </span>
            <span className="text-[11px] text-[#B5B5B5]">
              Demonstrating web app admin capabilities for lead management, content editing, and analytics.
            </span>
          </div>
        </div>
        <span className="text-[10px] font-mono bg-[#1A1A1A] text-[#FF303B] px-3 py-1 rounded border border-[#FF303B]/20">
          SYSTEM STATUS: ONLINE
        </span>
      </div>

      {/* Analytics Overview Cards */}
      <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
        {[
          { label: "Lead Enquiries", val: enquiries.length, icon: UserCheck, color: "text-[#FF303B]" },
          { label: "Active Members", val: "1,240", icon: Users, color: "text-white" },
          { label: "Estimated MRR", val: "₹18,60,000", icon: TrendingUp, color: "text-[#FF303B]" },
          { label: "Lead Conversion Rate", val: "72.4%", icon: Activity, color: "text-white" }
        ].map((card, idx) => {
          const IconComp = card.icon;
          return (
            <div key={idx} className="bg-[#141414] border border-[#1A1A1A] p-5 rounded-xl space-y-2">
              <div className="flex items-center justify-between text-xs text-[#B5B5B5]">
                <span>{card.label}</span>
                <IconComp className={`w-4 h-4 ${card.color}`} />
              </div>
              <div className="text-2xl font-black text-white">{card.val}</div>
            </div>
          );
        })}
      </div>

      {/* Dashboard Tabs Header */}
      <div className="flex border-b border-[#1A1A1A] gap-4">
        {[
          { id: "enquiries", label: "Lead Enquiries Manager" },
          { id: "schedule", label: "Timetable Schedule Editor" },
          { id: "trainers", label: "Trainers Roster" }
        ].map((tab) => (
          <button
            key={tab.id}
            onClick={() => setActiveTab(tab.id)}
            className={`pb-3 text-xs font-bold uppercase tracking-wider transition-colors relative ${
              activeTab === tab.id ? "text-[#FF303B]" : "text-[#B5B5B5] hover:text-white"
            }`}
          >
            {tab.label}
            {activeTab === tab.id && <span className="absolute bottom-0 left-0 right-0 h-0.5 bg-[#FF303B]"></span>}
          </button>
        ))}
      </div>

      {/* TAB 1: LEAD ENQUIRIES */}
      {activeTab === "enquiries" && (
        <div className="bg-[#141414] border border-[#1A1A1A] rounded-xl overflow-x-auto p-6 space-y-4">
          <div className="flex justify-between items-center mb-4">
            <h3 className="text-xs font-bold uppercase text-white tracking-wider">Incoming Membership Leads</h3>
            <span className="text-xs text-[#B5B5B5]">{enquiries.length} Enquiries Total</span>
          </div>
          <table className="w-full text-left text-xs border-collapse">
            <thead>
              <tr className="border-b border-white/10 text-[#B5B5B5] uppercase">
                <th className="py-3 px-3">Date</th>
                <th className="py-3 px-3">Name</th>
                <th className="py-3 px-3">Phone</th>
                <th className="py-3 px-3">Plan Requested</th>
                <th className="py-3 px-3">Status</th>
                <th className="py-3 px-3 text-right">Action</th>
              </tr>
            </thead>
            <tbody className="divide-y divide-white/5 text-[#B5B5B5]">
              {enquiries.map((e) => (
                <tr key={e.id} className="hover:bg-[#1A1A1A]">
                  <td className="py-3 px-3">{e.date}</td>
                  <td className="py-3 px-3 font-semibold text-white">{e.name}</td>
                  <td className="py-3 px-3">{e.phone}</td>
                  <td className="py-3 px-3 text-white">{e.plan}</td>
                  <td className="py-3 px-3">
                    <span className="bg-[#FF303B]/10 text-[#FF303B] px-2 py-0.5 rounded text-[10px] font-bold uppercase">
                      {e.status}
                    </span>
                  </td>
                  <td className="py-3 px-3 text-right">
                    <button
                      onClick={() => setEnquiries(enquiries.filter((item) => item.id !== e.id))}
                      className="text-xs text-red-400 hover:text-red-300 flex items-center gap-1 justify-end ml-auto"
                    >
                      <Trash2 className="w-3.5 h-3.5" /> Remove
                    </button>
                  </td>
                </tr>
              ))}
            </tbody>
          </table>
        </div>
      )}

      {/* TAB 2: SCHEDULE EDITOR */}
      {activeTab === "schedule" && (
        <div className="bg-[#141414] border border-[#1A1A1A] rounded-xl p-6 space-y-6">
          <div className="flex flex-col sm:flex-row justify-between sm:items-center gap-4 border-b border-white/5 pb-4">
            <h3 className="text-xs font-bold uppercase text-white tracking-wider">Dynamic Schedule Configurator</h3>
            <div className="flex gap-2">
              <input
                type="text"
                placeholder="e.g. 09:00 PM - 10:00 PM"
                value={newSlotTime}
                onChange={(e) => setNewSlotTime(e.target.value)}
                className="bg-[#1A1A1A] border border-white/10 px-3 py-1.5 rounded text-xs text-white focus:outline-none"
              />
              <button
                onClick={addScheduleRow}
                className="bg-[#FF303B] text-white px-3 py-1.5 rounded text-xs font-bold uppercase flex items-center gap-1"
              >
                <Plus className="w-3.5 h-3.5" /> Add Slot
              </button>
            </div>
          </div>

          <div className="overflow-x-auto">
            <table className="w-full text-center text-xs">
              <thead>
                <tr className="bg-[#1A1A1A] text-white uppercase">
                  <th className="py-2.5 px-2 text-left">Time</th>
                  <th className="py-2.5 px-2">Mon</th>
                  <th className="py-2.5 px-2">Tue</th>
                  <th className="py-2.5 px-2">Wed</th>
                  <th className="py-2.5 px-2">Thu</th>
                  <th className="py-2.5 px-2">Fri</th>
                  <th className="py-2.5 px-2">Sat</th>
                  <th className="py-2.5 px-2 text-right">Action</th>
                </tr>
              </thead>
              <tbody className="divide-y divide-white/5">
                {scheduleData.map((row, idx) => (
                  <tr key={idx}>
                    <td className="py-2.5 px-2 text-left text-white font-medium">{row.time}</td>
                    <td className="py-2.5 px-2">{row.mon}</td>
                    <td className="py-2.5 px-2">{row.tue}</td>
                    <td className="py-2.5 px-2">{row.wed}</td>
                    <td className="py-2.5 px-2">{row.thu}</td>
                    <td className="py-2.5 px-2">{row.fri}</td>
                    <td className="py-2.5 px-2 text-[#FF303B] font-bold">{row.sat}</td>
                    <td className="py-2.5 px-2 text-right">
                      <button
                        onClick={() => setScheduleData(scheduleData.filter((_, i) => i !== idx))}
                        className="text-red-400 text-[10px] uppercase font-bold"
                      >
                        Delete
                      </button>
                    </td>
                  </tr>
                ))}
              </tbody>
            </table>
          </div>
        </div>
      )}

      {/* TAB 3: TRAINERS ROSTER */}
      {activeTab === "trainers" && (
        <div className="bg-[#141414] border border-[#1A1A1A] rounded-xl p-6 space-y-4">
          <div className="flex justify-between items-center mb-4">
            <h3 className="text-xs font-bold uppercase text-white tracking-wider">Active Staff & Master Coaches</h3>
            <button className="bg-[#1A1A1A] border border-white/10 text-white px-3 py-1.5 rounded text-xs font-bold uppercase flex items-center gap-1">
              <Plus className="w-3.5 h-3.5" /> Add Staff
            </button>
          </div>
          <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
            {TRAINERS_DATA.map((t) => (
              <div key={t.id} className="bg-[#1A1A1A] p-4 rounded-lg flex items-center justify-between border border-white/5">
                <div>
                  <h4 className="text-sm font-bold text-white">{t.name}</h4>
                  <span className="text-xs text-[#FF303B]">{t.role}</span>
                </div>
                <div className="flex gap-2">
                  <button className="p-2 text-xs bg-[#141414] text-[#B5B5B5] hover:text-white rounded">
                    <Edit className="w-3.5 h-3.5" />
                  </button>
                </div>
              </div>
            ))}
          </div>
        </div>
      )}
    </div>
  );
}
```
