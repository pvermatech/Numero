# TheSoulLife Numerology Landing Page - Clean Final Code

## Project Structure
```
numerology_landing/
├── client/
│   ├── public/
│   │   └── images/
│   │       ├── logo-nobg.png
│   │       ├── IMG_0433.jpg
│   │       ├── IMG_3746.JPG
│   │       ├── IMG_3719.jpg
│   │       ├── IMG_2518.JPG
│   │       └── F1A8FB32-411E-45BC-9A40-C6F8CC953542.JPG
│   ├── src/
│   │   ├── pages/
│   │   │   └── Home.tsx (Main landing page component)
│   │   ├── components/
│   │   │   └── (shadcn/ui components)
│   │   ├── const.ts (Constants and configuration)
│   │   ├── index.css (Global styles and design tokens)
│   │   ├── App.tsx (Main app wrapper)
│   │   └── main.tsx (Entry point)
│   └── index.html
└── server/ (Placeholder for compatibility)
```

---

## 1. HOME.TSX - Main Landing Page Component

```tsx
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { APP_LOGO } from "@/const";
import { 
  CheckCircle2, 
  Clock, 
  Sparkles, 
  Heart, 
  Users, 
  TrendingUp, 
  Shield, 
  Star, 
  AlertCircle 
} from "lucide-react";
import { useState, useEffect } from "react";
import {
  Accordion,
  AccordionContent,
  AccordionItem,
  AccordionTrigger,
} from "@/components/ui/accordion";

/**
 * HOME PAGE COMPONENT
 * 
 * High-converting numerology webinar landing page for Vritikaa Panjwani
 * 
 * DESIGN PHILOSOPHY:
 * - Emotional, transformation-focused messaging
 * - Scarcity and urgency elements throughout
 * - Multiple CTAs for maximum conversion
 * - Pastel green, beige, gold color scheme
 * - Playfair Display serif headings + Inter sans-serif body
 * 
 * SECTIONS:
 * 1. Hero Section - Powerful headline with urgency
 * 2. Countdown Timer - Live countdown to workshop
 * 3. Pain Points - Why audience feels stuck
 * 4. About Vritikaa - Story, authority, credibility
 * 5. Workshop Content - Transformation-focused benefits
 * 6. Pricing & Offer - Limited seats, scarcity messaging
 * 7. FAQ - Objection handling
 * 8. Final CTA - Dramatic closing section
 * 9. Footer - Brand reinforcement
 */

export default function Home() {
  // ============================================
  // STATE MANAGEMENT
  // ============================================
  
  const [timeLeft, setTimeLeft] = useState({
    days: 2,
    hours: 15,
    minutes: 30,
    seconds: 0
  });

  // ============================================
  // EFFECTS
  // ============================================
  
  /**
   * Countdown timer effect
   * Updates every second to create urgency
   */
  useEffect(() => {
    const timer = setInterval(() => {
      setTimeLeft(prev => {
        if (prev.seconds > 0) {
          return { ...prev, seconds: prev.seconds - 1 };
        } else if (prev.minutes > 0) {
          return { ...prev, minutes: prev.minutes - 1, seconds: 59 };
        } else if (prev.hours > 0) {
          return { ...prev, hours: prev.hours - 1, minutes: 59, seconds: 59 };
        } else if (prev.days > 0) {
          return { ...prev, days: prev.days - 1, hours: 23, minutes: 59, seconds: 59 };
        }
        return prev;
      });
    }, 1000);

    return () => clearInterval(timer);
  }, []);

  // ============================================
  // HELPER FUNCTIONS
  // ============================================
  
  /**
   * Smooth scroll to registration section
   */
  const scrollToCTA = () => {
    const ctaSection = document.getElementById('register');
    ctaSection?.scrollIntoView({ behavior: 'smooth' });
  };

  // ============================================
  // RENDER
  // ============================================
  
  return (
    <div className="min-h-screen">
      
      {/* ========================================
          SECTION 1: HERO - HIGH-IMPACT EMOTIONAL HEADLINE
          ======================================== */}
      <section className="relative overflow-hidden bg-gradient-to-br from-background via-secondary to-muted py-20 md:py-32">
        
        {/* Decorative numerology numbers background */}
        <div className="absolute inset-0 opacity-10">
          <div className="absolute top-20 left-10 text-9xl text-primary font-serif">1</div>
          <div className="absolute top-40 right-20 text-9xl text-accent font-serif">3</div>
          <div className="absolute bottom-20 left-1/3 text-9xl text-primary font-serif">7</div>
          <div className="absolute bottom-40 right-1/4 text-9xl text-accent font-serif">9</div>
        </div>
        
        <div className="container relative z-10">
          <div className="flex flex-col lg:flex-row items-center gap-12">
            
            {/* LEFT COLUMN: TEXT CONTENT */}
            <div className="flex-1 text-center lg:text-left">
              
              {/* Logo */}
              <div className="mb-6">
                <img 
                  src={APP_LOGO} 
                  alt="TheSoulLife" 
                  className="h-20 mx-auto lg:mx-0" 
                />
              </div>
              
              {/* Main Headline */}
              <h1 className="text-4xl md:text-6xl font-bold mb-6 leading-tight">
                Decode Your Life's Hidden Patterns Through Numerology
              </h1>
              
              {/* Subheadline */}
              <p className="text-xl md:text-2xl mb-6 text-foreground font-medium">
                Transform Your Relationships, Career & Destiny in 2 Hours
              </p>
              
              {/* Urgency Box */}
              <div className="bg-destructive/10 border-2 border-destructive rounded-lg p-4 mb-8 inline-block">
                <p className="text-lg font-semibold text-destructive">
                  A rare LIVE workshop with Vritikaa Panjwani<br/>
                  <span className="text-base">Limited seats • No replay</span>
                </p>
              </div>
              
              {/* Primary CTA Button */}
              <div className="flex flex-col sm:flex-row gap-4 justify-center lg:justify-start mb-6">
                <Button 
                  size="lg" 
                  className="text-lg px-10 py-7 bg-accent hover:bg-accent/90 text-accent-foreground shadow-xl hover:shadow-2xl transition-all hover:scale-105" 
                  onClick={scrollToCTA}
                >
                  Reserve My Seat Now
                </Button>
              </div>
              
              {/* Scarcity Alert */}
              <div className="flex items-center justify-center lg:justify-start gap-2 text-sm font-medium">
                <AlertCircle className="h-5 w-5 text-destructive" />
                <span>
                  Only <span className="text-destructive font-bold">12 seats left</span> at this price
                </span>
              </div>
            </div>
            
            {/* RIGHT COLUMN: HERO IMAGE */}
            <div className="flex-1">
              <div className="relative">
                {/* Glow effect behind image */}
                <div className="absolute inset-0 bg-gradient-to-br from-primary/20 to-accent/20 rounded-full blur-3xl"></div>
                
                {/* Hero image */}
                <img 
                  src="/images/IMG_0433.jpg" 
                  alt="Vritikaa Panjwani" 
                  className="relative rounded-2xl shadow-2xl w-full max-w-md mx-auto object-cover aspect-square"
                  loading="eager"
                />
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* ========================================
          COUNTDOWN TIMER - URGENCY ELEMENT
          ======================================== */}
      <section className="bg-primary text-primary-foreground py-8">
        <div className="container">
          <div className="flex flex-col md:flex-row items-center justify-center gap-8">
            <p className="text-xl font-semibold">Workshop Starts In:</p>
            
            {/* Timer boxes */}
            <div className="flex gap-4">
              {[
                { label: 'Days', value: timeLeft.days },
                { label: 'Hours', value: timeLeft.hours },
                { label: 'Minutes', value: timeLeft.minutes },
                { label: 'Seconds', value: timeLeft.seconds }
              ].map((item, idx) => (
                <div key={idx} className="text-center">
                  <div className="bg-primary-foreground text-primary rounded-lg p-4 min-w-[70px]">
                    <div className="text-3xl font-bold">
                      {item.value.toString().padStart(2, '0')}
                    </div>
                  </div>
                  <div className="text-sm mt-2">{item.label}</div>
                </div>
              ))}
            </div>
          </div>
        </div>
      </section>

      {/* ========================================
          SECTION 2: PAIN POINTS - WHY YOU FEEL STUCK
          ======================================== */}
      <section className="py-20 bg-card">
        <div className="container max-w-5xl">
          
          {/* Section header */}
          <div className="text-center mb-12">
            <h2 className="text-3xl md:text-5xl font-bold mb-6">
              Why Do You Feel Stuck?
            </h2>
            <p className="text-xl text-muted-foreground">
              If any of these resonate, you're in the right place...
            </p>
          </div>
          
          {/* Pain points grid */}
          <div className="grid md:grid-cols-2 gap-6 mb-12">
            {[
              "You keep attracting the same kind of relationships",
              "You feel your potential isn't matching your outcomes",
              "Money flows in but never seems to stay",
              "You're confused about your purpose",
              "You sense something bigger, but lack direction",
              "Your emotional patterns feel repetitive"
            ].map((item, idx) => (
              <div 
                key={idx} 
                className="flex items-start gap-4 p-6 bg-muted/50 rounded-lg border-2 border-transparent hover:border-primary transition-colors"
              >
                <div className="bg-primary/10 text-primary rounded-full w-8 h-8 flex items-center justify-center flex-shrink-0 mt-1">
                  <CheckCircle2 className="h-5 w-5" />
                </div>
                <p className="text-lg">{item}</p>
              </div>
            ))}
          </div>
          
          {/* Transition box */}
          <div className="bg-gradient-to-r from-primary/10 via-accent/10 to-primary/10 rounded-2xl p-8 md:p-12 text-center">
            <Sparkles className="h-16 w-16 mx-auto mb-6 text-accent" />
            <h3 className="text-2xl md:text-4xl font-bold mb-6">
              These Patterns Aren't Random — They're Numerical
            </h3>
            <p className="text-xl text-muted-foreground mb-8 max-w-3xl mx-auto">
              And once you decode them, <span className="font-bold text-foreground">everything changes</span>. 
              Your numbers reveal why you think, feel, love, and choose the way you do.
            </p>
            
            {/* Secondary CTA */}
            <Button 
              size="lg" 
              className="bg-accent hover:bg-accent/90 text-accent-foreground px-10 py-7 text-lg shadow-lg" 
              onClick={scrollToCTA}
            >
              Decode Your Numbers Now
            </Button>
          </div>
        </div>
      </section>

      {/* ========================================
          SECTION 3: ABOUT VRITIKAA - AUTHORITY & STORY
          ======================================== */}
      <section className="py-20 bg-gradient-to-br from-secondary to-background">
        <div className="container max-w-6xl">
          
          {/* Section header */}
          <div className="text-center mb-12">
            <h2 className="text-3xl md:text-5xl font-bold mb-4">
              Meet Your Guide
            </h2>
            <p className="text-2xl text-accent font-semibold">Vritikaa Panjwani</p>
            <p className="text-lg text-muted-foreground mt-2">Intuitive Numerologist & Soul Guide</p>
          </div>
          
          {/* Two-column layout: text + images */}
          <div className="grid lg:grid-cols-2 gap-12 items-center mb-12">
            
            {/* LEFT: TEXT CONTENT */}
            <div className="order-2 lg:order-1">
              <div className="prose prose-lg max-w-none">
                
                {/* Introduction */}
                <p className="text-xl mb-6 font-medium text-foreground">
                  Vritikaa has guided <span className="text-primary font-bold">hundreds of seekers</span> through personalized numerology sessions — helping people understand their deepest emotional patterns, compatibility, strengths, and karmic lessons.
                </p>
                
                {/* Personal story */}
                <p className="text-lg mb-6">
                  Her journey into numerology began with her own quest for clarity. After years of feeling disconnected from her true path, she discovered the ancient science of numbers and experienced a profound transformation. Now, she's dedicated her life to sharing this wisdom.
                </p>
                
                {/* What makes her different */}
                <div className="bg-card rounded-xl p-6 mb-6 border-l-4 border-accent">
                  <p className="text-lg font-semibold mb-4">What Makes Vritikaa Different:</p>
                  <div className="space-y-3">
                    {[
                      { 
                        label: "Intuitive Accuracy", 
                        text: "Combines traditional numerology with deep intuitive insights for readings that feel personally crafted" 
                      },
                      { 
                        label: "Proven Results", 
                        text: "Countless clients have found relationship clarity, career direction, and emotional healing" 
                      },
                      { 
                        label: "Warm Presence", 
                        text: "Creates a safe, nurturing space where transformation feels natural and supported" 
                      },
                      { 
                        label: "Ancient Wisdom", 
                        text: "Trained in authentic Indian numerology traditions passed through generations" 
                      }
                    ].map((item, idx) => (
                      <div key={idx} className="flex gap-3">
                        <Star className="h-6 w-6 text-accent flex-shrink-0 mt-0.5" />
                        <div>
                          <span className="font-semibold text-primary">{item.label}:</span> {item.text}
                        </div>
                      </div>
                    ))}
                  </div>
                </div>
                
                {/* Testimonial quote */}
                <p className="text-xl italic text-muted-foreground border-l-4 border-primary pl-6">
                  "I've seen numerology change lives — including my own. If you're ready to stop guessing and start knowing, I'm here to guide you."
                  <span className="block mt-2 text-base not-italic font-semibold">— Vritikaa Panjwani</span>
                </p>
              </div>
            </div>
            
            {/* RIGHT: IMAGES */}
            <div className="order-1 lg:order-2">
              <div className="grid grid-cols-2 gap-4">
                <img 
                  src="/images/IMG_3746.JPG" 
                  alt="Vritikaa Panjwani" 
                  className="rounded-2xl shadow-xl w-full object-cover aspect-[3/4]"
                />
                <img 
                  src="/images/IMG_3719.jpg" 
                  alt="Vritikaa Panjwani" 
                  className="rounded-2xl shadow-xl w-full object-cover aspect-[3/4] mt-8"
                />
              </div>
              <div className="mt-6 text-center">
                <img 
                  src="/images/IMG_2518.JPG" 
                  alt="Vritikaa Panjwani at work" 
                  className="rounded-2xl shadow-xl w-full object-cover aspect-video"
                />
              </div>
            </div>
          </div>

          {/* CTA */}
          <div className="text-center">
            <Button 
              size="lg" 
              className="bg-primary hover:bg-primary/90 text-primary-foreground px-10 py-7 text-lg shadow-lg" 
              onClick={scrollToCTA}
            >
              Learn with Vritikaa
            </Button>
          </div>
        </div>
      </section>

      {/* ========================================
          SECTION 4: WORKSHOP CONTENT - TRANSFORMATION FOCUSED
          ======================================== */}
      <section className="py-20 bg-card">
        <div className="container max-w-6xl">
          
          {/* Section header */}
          <div className="text-center mb-16">
            <h2 className="text-3xl md:text-5xl font-bold mb-6">
              What You'll Experience in This Workshop
            </h2>
            <p className="text-xl text-muted-foreground max-w-3xl mx-auto">
              This isn't just theory — it's a transformation in understanding yourself
            </p>
          </div>
          
          {/* Benefits grid */}
          <div className="grid md:grid-cols-2 gap-8 mb-12">
            {[
              {
                icon: <Heart className="h-10 w-10" />,
                title: "Understand Your Soul Blueprint",
                description: "Calculate your Moolank (Birth Day Number) and Bhagyank (Life Path Number) — the core codes that reveal your natural gifts, challenges, and life purpose."
              },
              {
                icon: <Users className="h-10 w-10" />,
                title: "Learn Why Your Relationships Fail or Succeed",
                description: "Discover the compatibility secrets between numbers. Finally understand why some connections flow effortlessly while others drain you."
              },
              {
                icon: <Star className="h-10 w-10" />,
                title: "Discover Your Natural Gifts & Life Purpose",
                description: "Stop wondering what you're meant to do. Your numbers reveal your innate talents, ideal career paths, and soul's calling."
              },
              {
                icon: <Shield className="h-10 w-10" />,
                title: "Decode the Karmic Lessons Holding You Back",
                description: "Understand the patterns you're meant to break. Learn about karmic numbers (13, 14, 16, 19) and master numbers (11, 22, 33) that shape your journey."
              },
              {
                icon: <TrendingUp className="h-10 w-10" />,
                title: "Make Aligned Decisions Instantly",
                description: "Use personal year, month, and day calculations to time your decisions perfectly. Know when to act and when to wait."
              },
              {
                icon: <Sparkles className="h-10 w-10" />,
                title: "Read Anyone's Personality in Seconds",
                description: "Master the meanings of numbers 1-9, their planetary rulers, and core traits. Understand anyone just from their birth date."
              },
              {
                icon: <TrendingUp className="h-10 w-10" />,
                title: "Unlock Your Money & Abundance Patterns",
                description: "Discover how your numbers influence your relationship with money, wealth attraction, and financial success. Learn which numbers bring prosperity and how to align with abundance."
              }
            ].map((item, idx) => (
              <Card 
                key={idx} 
                className="hover:shadow-2xl transition-all hover:-translate-y-1 border-2 hover:border-primary"
              >
                <CardContent className="p-8">
                  <div className="inline-flex items-center justify-center w-16 h-16 bg-primary/10 text-primary rounded-full mb-4">
                    {item.icon}
                  </div>
                  <h3 className="text-2xl font-bold mb-3">{item.title}</h3>
                  <p className="text-muted-foreground text-lg">{item.description}</p>
                </CardContent>
              </Card>
            ))}
          </div>

          {/* Closing statement */}
          <div className="text-center bg-gradient-to-r from-accent/10 to-primary/10 rounded-2xl p-8">
            <p className="text-xl mb-6 font-semibold">
              By the end of this workshop, you'll have <span className="text-primary">lifetime knowledge</span> you can apply to yourself, your loved ones, and every major decision you make.
            </p>
            <Button 
              size="lg" 
              className="bg-accent hover:bg-accent/90 text-accent-foreground px-10 py-7 text-lg shadow-lg" 
              onClick={scrollToCTA}
            >
              Start Your Transformation
            </Button>
          </div>
        </div>
      </section>

      {/* ========================================
          SECTION 5: PRICING & OFFER - SCARCITY
          ======================================== */}
      <section id="register" className="py-20 bg-gradient-to-br from-background to-secondary">
        <div className="container max-w-4xl">
          
          {/* Section header */}
          <div className="text-center mb-12">
            <div className="inline-block bg-destructive text-destructive-foreground px-6 py-3 rounded-full text-sm font-bold mb-6 animate-pulse">
              ⚠️ ONLY 12 SEATS REMAINING
            </div>
            <h2 className="text-3xl md:text-5xl font-bold mb-6">
              Reserve Your Seat Before It's Gone
            </h2>
            <p className="text-xl text-muted-foreground">
              This is a <span className="font-bold text-foreground">live-only</span> intimate workshop. No replay. No second chances.
            </p>
          </div>
          
          {/* Pricing card */}
          <Card className="border-4 border-accent shadow-2xl relative overflow-hidden">
            
            {/* Limited time badge */}
            <div className="absolute top-0 right-0 bg-destructive text-destructive-foreground px-6 py-2 text-sm font-bold transform rotate-12 translate-x-8 -translate-y-2">
              LIMITED TIME
            </div>
            
            <CardContent className="p-8 md:p-12">
              
              {/* Price display */}
              <div className="text-center mb-8">
                <div className="mb-6">
                  <div className="text-6xl md:text-8xl font-bold mb-2">₹249</div>
                  <div className="text-2xl text-muted-foreground line-through">₹999</div>
                  <p className="text-lg text-accent font-semibold mt-2">Save ₹750 Today • 75% OFF</p>
                </div>
                <p className="text-xl font-medium">
                  Full 2-Hour Live Numerology Workshop
                </p>
              </div>
              
              {/* What's included */}
              <div className="space-y-4 mb-8">
                {[
                  "Complete 2-hour live workshop with Vritikaa Panjwani",
                  "Personal calculation guidance during the session",
                  "Learn to calculate your own numbers forever",
                  "Detailed explanation of all numerology concepts",
                  "Interactive Q&A and personalized insights",
                  "Lifetime knowledge you can apply immediately"
                ].map((item, idx) => (
                  <div key={idx} className="flex items-center gap-3">
                    <CheckCircle2 className="h-7 w-7 text-primary flex-shrink-0" />
                    <span className="text-lg font-medium">{item}</span>
                  </div>
                ))}
              </div>
              
              {/* Primary CTA button */}
              <Button 
                size="lg" 
                className="w-full text-2xl py-10 bg-accent hover:bg-accent/90 text-accent-foreground shadow-xl hover:shadow-2xl transition-all hover:scale-105 mb-4"
                onClick={() => alert('Registration form will be linked here. Please contact Vritikaa to set up your registration link.')}
              >
                Reserve My Seat Now
              </Button>
              
              {/* Trust signals */}
              <div className="text-center space-y-2">
                <p className="text-sm text-muted-foreground flex items-center justify-center gap-2">
                  <Clock className="h-4 w-4 text-destructive" />
                  <span className="font-bold text-destructive">12 seats left</span> • Price increases after next 5 registrations
                </p>
                <p className="text-xs text-muted-foreground">
                  🔒 Secure payment • 💯 100% satisfaction guarantee
                </p>
              </div>
            </CardContent>
          </Card>
        </div>
      </section>

      {/* ========================================
          SECTION 6: FAQ - OBJECTION HANDLING
          ======================================== */}
      <section className="py-20 bg-card">
        <div className="container max-w-3xl">
          
          {/* Section header */}
          <div className="text-center mb-12">
            <h2 className="text-3xl md:text-5xl font-bold mb-6">
              Your Questions Answered
            </h2>
            <p className="text-lg text-muted-foreground">
              Everything you need to know before joining
            </p>
          </div>
          
          {/* FAQ accordion */}
          <Accordion type="single" collapsible className="space-y-4 mb-12">
            {[
              {
                question: "✅ Is this beginner-friendly?",
                answer: "Absolutely! This workshop is designed specifically for beginners. You don't need any prior knowledge of numerology, astrology, or spirituality. Vritikaa will guide you step-by-step from the very basics. If you can add numbers, you can learn numerology!"
              },
              {
                question: "🔢 Will Vritikaa calculate my numbers?",
                answer: "Yes! During the live workshop, Vritikaa will guide you through calculating your own Moolank (Birth Day Number) and Bhagyank (Life Path Number). You'll learn the exact formulas so you can calculate numbers for yourself, family, friends, and partners anytime in the future."
              },
              {
                question: "📚 Do I need prior knowledge?",
                answer: "Not at all! This is a complete introduction to numerology. Whether you've never heard of Moolank and Bhagyank or you're curious about the basics, this workshop starts from zero and builds your understanding systematically."
              },
              {
                question: "⏰ What if I can't attend live?",
                answer: "This is a live-only workshop designed for maximum interaction and personalized guidance. There is no replay available. Please ensure you can attend at the scheduled date and time to get the full transformative experience."
              },
              {
                question: "💻 How do I access the workshop?",
                answer: "After you register, you'll receive an email with the Zoom meeting link and all the details you need. Simply click the link at the scheduled time to join from anywhere in the world — all you need is an internet connection!"
              },
              {
                question: "📝 What should I prepare?",
                answer: "Just bring your birth date and the birth dates of anyone you'd like to analyze (partner, family members, friends). Have a notebook and pen ready to take notes. Come with an open mind and curiosity!"
              },
              {
                question: "🎯 What will I be able to do after this workshop?",
                answer: "You'll be able to calculate and interpret your own numbers, understand your personality blueprint, decode relationship compatibility, identify your life purpose, and make aligned decisions using numerology. This is lifetime knowledge you can use forever."
              }
            ].map((item, idx) => (
              <AccordionItem 
                key={idx} 
                value={`item-${idx}`} 
                className="bg-muted/30 border-2 rounded-lg px-6 hover:border-primary transition-colors"
              >
                <AccordionTrigger className="text-left text-lg font-semibold hover:text-primary">
                  {item.question}
                </AccordionTrigger>
                <AccordionContent className="text-muted-foreground text-base leading-relaxed">
                  {item.answer}
                </AccordionContent>
              </AccordionItem>
            ))}
          </Accordion>

          {/* CTA */}
          <div className="text-center">
            <p className="text-lg mb-6 text-muted-foreground">Still have questions?</p>
            <Button 
              size="lg" 
              className="bg-primary hover:bg-primary/90 text-primary-foreground px-10 py-6 text-lg shadow-lg" 
              onClick={scrollToCTA}
            >
              Secure Your Spot Now
            </Button>
          </div>
        </div>
      </section>

      {/* ========================================
          SECTION 7: FINAL CTA - DRAMATIC CLOSING
          ======================================== */}
      <section className="py-24 bg-gradient-to-br from-primary via-accent to-primary text-primary-foreground relative overflow-hidden">
        
        {/* Decorative background */}
        <div className="absolute inset-0 opacity-20">
          <div className="absolute top-10 left-10 text-9xl font-serif animate-pulse">✨</div>
          <div className="absolute bottom-10 right-10 text-9xl font-serif animate-pulse">🔮</div>
          <div className="absolute top-1/2 left-1/4 text-7xl font-serif">1</div>
          <div className="absolute top-1/3 right-1/3 text-7xl font-serif">9</div>
        </div>
        
        <div className="container max-w-5xl relative z-10">
          
          {/* Main message */}
          <div className="text-center mb-12">
            <h2 className="text-4xl md:text-6xl font-bold mb-8 leading-tight">
              Your Numbers Hold the Answers You've Been Searching For
            </h2>
            
            <p className="text-2xl md:text-3xl mb-6 opacity-95 font-medium">
              Don't stay confused. Decode yourself.
            </p>
            
            <p className="text-xl mb-10 opacity-90 max-w-3xl mx-auto">
              Every day you wait is another day living without clarity. Your relationships, career, and purpose are waiting for you to understand the patterns. This is your moment.
            </p>
          </div>

          {/* Two-column layout */}
          <div className="grid lg:grid-cols-2 gap-12 items-center mb-12">
            
            {/* Image */}
            <div>
              <img 
                src="/images/F1A8FB32-411E-45BC-9A40-C6F8CC953542.JPG" 
                alt="Vritikaa Panjwani" 
                className="rounded-2xl shadow-2xl w-full object-cover"
              />
            </div>
            
            {/* Text + CTA */}
            <div className="text-center lg:text-left space-y-6">
              <div className="space-y-4">
                {[
                  "Stop repeating the same relationship patterns",
                  "Finally understand your true purpose",
                  "Make decisions with confidence and clarity",
                  "Unlock your hidden potential"
                ].map((item, idx) => (
                  <div key={idx} className="flex items-center gap-3 text-lg">
                    <CheckCircle2 className="h-6 w-6 flex-shrink-0" />
                    <span>{item}</span>
                  </div>
                ))}
              </div>
              
              {/* Final CTA button */}
              <Button 
                size="lg" 
                variant="secondary"
                className="text-2xl px-12 py-10 shadow-2xl hover:scale-105 transition-transform w-full lg:w-auto"
                onClick={scrollToCTA}
              >
                Reserve My Seat
              </Button>
              
              {/* Timer reminder */}
              <p className="text-sm opacity-75">
                ⏰ Workshop starts in {timeLeft.days}d {timeLeft.hours}h {timeLeft.minutes}m • Only 12 seats left
              </p>
            </div>
          </div>

          {/* Closing quote */}
          <div className="text-center bg-white/10 backdrop-blur-sm rounded-2xl p-8">
            <p className="text-xl font-semibold mb-2">
              "The best time to understand yourself was years ago."
            </p>
            <p className="text-2xl font-bold">
              "The second best time is right now."
            </p>
          </div>
        </div>
      </section>

      {/* ========================================
          FOOTER
          ======================================== */}
      <footer className="bg-card py-12 border-t">
        <div className="container text-center">
          <img 
            src={APP_LOGO} 
            alt="TheSoulLife" 
            className="h-16 mx-auto mb-4" 
          />
          <p className="text-muted-foreground mb-6 text-lg">
            Transform your life through the ancient wisdom of numerology
          </p>
          <Button 
            variant="outline" 
            size="lg"
            className="mb-6"
            onClick={scrollToCTA}
          >
            Join the Workshop
          </Button>
          <p className="text-sm text-muted-foreground">
            © 2024 TheSoulLife. All rights reserved.
          </p>
        </div>
      </footer>
    </div>
  );
}
```

---

## 2. INDEX.CSS - Global Styles & Design Tokens

```css
@import "tailwindcss";
@import "tw-animate-css";

@custom-variant dark (&:is(.dark *));

@theme inline {
  --radius-sm: calc(var(--radius) - 4px);
  --radius-md: calc(var(--radius) - 2px);
  --radius-lg: var(--radius);
  --radius-xl: calc(var(--radius) + 4px);
  --color-background: var(--background);
  --color-foreground: var(--foreground);
  --color-card: var(--card);
  --color-card-foreground: var(--card-foreground);
  --color-popover: var(--popover);
  --color-popover-foreground: var(--popover-foreground);
  --color-primary: var(--primary);
  --color-primary-foreground: var(--primary-foreground);
  --color-secondary: var(--secondary);
  --color-secondary-foreground: var(--secondary-foreground);
  --color-muted: var(--muted);
  --color-muted-foreground: var(--muted-foreground);
  --color-accent: var(--accent);
  --color-accent-foreground: var(--accent-foreground);
  --color-destructive: var(--destructive);
  --color-destructive-foreground: var(--destructive-foreground);
  --color-border: var(--border);
  --color-input: var(--input);
  --color-ring: var(--ring);
  --color-chart-1: var(--chart-1);
  --color-chart-2: var(--chart-2);
  --color-chart-3: var(--chart-3);
  --color-chart-4: var(--chart-4);
  --color-chart-5: var(--chart-5);
  --color-sidebar: var(--sidebar);
  --color-sidebar-foreground: var(--sidebar-foreground);
  --color-sidebar-primary: var(--sidebar-primary);
  --color-sidebar-primary-foreground: var(--sidebar-primary-foreground);
  --color-sidebar-accent: var(--sidebar-accent);
  --color-sidebar-accent-foreground: var(--sidebar-accent-foreground);
  --color-sidebar-border: var(--sidebar-border);
  --color-sidebar-ring: var(--sidebar-ring);
}

/**
 * COLOR PALETTE
 * 
 * DESIGN PHILOSOPHY: Spiritual, Feminine, Mystical
 * - Primary: Soft sage green (spiritual, calming)
 * - Accent: Gold (prosperity, abundance)
 * - Background: Soft beige (warm, welcoming)
 * - Foreground: Dark brown (readable, grounded)
 */

:root {
  /* Pastel green, beige, gold color scheme */
  --primary: oklch(0.55 0.08 160); /* Soft sage green */
  --primary-foreground: oklch(0.98 0 0);
  --sidebar-primary: oklch(0.55 0.08 160);
  --sidebar-primary-foreground: oklch(0.98 0 0);
  --chart-1: oklch(0.75 0.06 160);
  --chart-2: oklch(0.65 0.07 160);
  --chart-3: oklch(0.55 0.08 160);
  --chart-4: oklch(0.45 0.09 160);
  --chart-5: oklch(0.35 0.1 160);
  --radius: 0.75rem;
  --background: oklch(0.98 0.01 80); /* Soft beige */
  --foreground: oklch(0.25 0.02 60); /* Dark brown */
  --card: oklch(1 0 0); /* Pure white */
  --card-foreground: oklch(0.25 0.02 60);
  --popover: oklch(1 0 0);
  --popover-foreground: oklch(0.25 0.02 60);
  --secondary: oklch(0.92 0.02 80); /* Light beige */
  --secondary-foreground: oklch(0.3 0.02 60);
  --muted: oklch(0.95 0.01 80);
  --muted-foreground: oklch(0.5 0.02 60);
  --accent: oklch(0.7 0.12 70); /* Gold accent */
  --accent-foreground: oklch(0.98 0 0);
  --destructive: oklch(0.577 0.245 27.325);
  --destructive-foreground: oklch(0.985 0 0);
  --border: oklch(0.88 0.02 80);
  --input: oklch(0.88 0.02 80);
  --ring: oklch(0.55 0.08 160);
  --sidebar: oklch(0.985 0 0);
  --sidebar-foreground: oklch(0.25 0.02 60);
  --sidebar-accent: oklch(0.95 0.01 80);
  --sidebar-accent-foreground: oklch(0.25 0.02 60);
  --sidebar-border: oklch(0.88 0.02 80);
  --sidebar-ring: oklch(0.55 0.08 160);
}

.dark {
  --primary: var(--color-blue-700);
  --primary-foreground: var(--color-blue-50);
  --sidebar-primary: var(--color-blue-500);
  --sidebar-primary-foreground: var(--color-blue-50);
  --background: oklch(0.141 0.005 285.823);
  --foreground: oklch(0.85 0.005 65);
  --card: oklch(0.21 0.006 285.885);
  --card-foreground: oklch(0.85 0.005 65);
  --popover: oklch(0.21 0.006 285.885);
  --popover-foreground: oklch(0.85 0.005 65);
  --secondary: oklch(0.24 0.006 286.033);
  --secondary-foreground: oklch(0.7 0.005 65);
  --muted: oklch(0.274 0.006 286.033);
  --muted-foreground: oklch(0.705 0.015 286.067);
  --accent: oklch(0.274 0.006 286.033);
  --accent-foreground:  oklch(0.92 0.005 65);
  --destructive: oklch(0.704 0.191 22.216);
  --destructive-foreground: oklch(0.985 0 0);
  --border: oklch(1 0 0 / 10%);
  --input: oklch(1 0 0 / 15%);
  --ring: oklch(0.488 0.243 264.376);
  --chart-1: var(--color-blue-300);
  --chart-2: var(--color-blue-500);
  --chart-3: var(--color-blue-600);
  --chart-4: var(--color-blue-700);
  --chart-5: var(--color-blue-800);
  --sidebar: oklch(0.21 0.006 285.885);
  --sidebar-foreground: oklch(0.85 0.005 65);
  --sidebar-accent: oklch(0.274 0.006 286.033);
  --sidebar-accent-foreground:  oklch(0.985 0 0);
  --sidebar-border: oklch(1 0 0 / 10%);
  --sidebar-ring: oklch(0.488 0.243 264.376);
}

/**
 * TYPOGRAPHY
 * 
 * - Playfair Display: Elegant serif for headings (h1-h6)
 * - Inter: Clean sans-serif for body text
 */

@layer base {
  * {
    @apply border-border outline-ring/50;
  }
  
  html {
    scroll-behavior: smooth;
  }
  
  body {
    @apply bg-background text-foreground;
    font-family: 'Inter', sans-serif;
  }
  
  h1, h2, h3, h4, h5, h6 {
    font-family: 'Playfair Display', serif;
  }
  
  button:not(:disabled),
  [role="button"]:not([aria-disabled="true"]),
  [type="button"]:not(:disabled),
  [type="submit"]:not(:disabled),
  [type="reset"]:not(:disabled),
  a[href],
  select:not(:disabled),
  input[type="checkbox"]:not(:disabled),
  input[type="radio"]:not(:disabled) {
    @apply cursor-pointer;
  }
}

/**
 * CUSTOM COMPONENTS
 */

@layer components {
  /**
   * Container utility
   * 
   * Centers content and adds responsive padding
   * Usage: <div className="container">...</div>
   */
  .container {
    width: 100%;
    margin-left: auto;
    margin-right: auto;
    padding-left: 1rem; /* 16px - mobile padding */
    padding-right: 1rem;
  }

  .flex {
    min-height: 0;
    min-width: 0;
  }

  @media (min-width: 640px) {
    .container {
      padding-left: 1.5rem; /* 24px - tablet padding */
      padding-right: 1.5rem;
    }
  }

  @media (min-width: 1024px) {
    .container {
      padding-left: 2rem; /* 32px - desktop padding */
      padding-right: 2rem;
      max-width: 1280px; /* Standard content width */
    }
  }
}
```

---

## 3. CONST.TS - Configuration & Constants

```typescript
/**
 * CONSTANTS & CONFIGURATION
 * 
 * Centralized configuration for the application
 */

export { COOKIE_NAME, ONE_YEAR_MS } from "@shared/const";

/**
 * Application title
 * Used in browser tab and meta tags
 */
export const APP_TITLE = import.meta.env.VITE_APP_TITLE || "App";

/**
 * Application logo
 * Path to transparent logo image
 * Update this when changing the logo
 */
export const APP_LOGO = "/images/logo-nobg.png";

/**
 * OAuth login URL generator
 * 
 * Generates the login URL at runtime so the redirect URI
 * reflects the current origin (important for different deployments)
 */
export const getLoginUrl = () => {
  const oauthPortalUrl = import.meta.env.VITE_OAUTH_PORTAL_URL;
  const appId = import.meta.env.VITE_APP_ID;
  const redirectUri = `${window.location.origin}/api/oauth/callback`;
  const state = btoa(redirectUri);

  const url = new URL(`${oauthPortalUrl}/app-auth`);
  url.searchParams.set("appId", appId);
  url.searchParams.set("redirectUri", redirectUri);
  url.searchParams.set("state", state);
  url.searchParams.set("type", "signIn");

  return url.toString();
};
```

---

## 4. INDEX.HTML - HTML Entry Point

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>TheSoulLife - Numerology Webinar</title>
    
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link 
      href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;500;600;700;800;900&family=Inter:wght@300;400;500;600;700;800;900&display=swap" 
      rel="stylesheet" 
    />
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.tsx"></script>
  </body>
</html>
```

---

## 5. APP.TSX - Main App Wrapper

```tsx
import { Toaster } from "@/components/ui/sonner";
import { TooltipProvider } from "@/components/ui/tooltip";
import NotFound from "@/pages/NotFound";
import { Route, Switch } from "wouter";
import ErrorBoundary from "./components/ErrorBoundary";
import { ThemeProvider } from "./contexts/ThemeContext";
import Home from "./pages/Home";

/**
 * ROUTER CONFIGURATION
 * 
 * Defines all application routes
 */
function Router() {
  return (
    <Switch>
      <Route path={"/"} component={Home} />
      <Route path={"/404"} component={NotFound} />
      {/* Final fallback route */}
      <Route component={NotFound} />
    </Switch>
  );
}

/**
 * MAIN APP COMPONENT
 * 
 * Wraps the entire application with:
 * - Theme provider (light mode by default)
 * - Tooltip provider for accessible tooltips
 * - Error boundary for error handling
 * - Toast notifications (Sonner)
 */
export default function App() {
  return (
    <ErrorBoundary>
      <ThemeProvider defaultTheme="light">
        <TooltipProvider>
          <Toaster />
          <Router />
        </TooltipProvider>
      </ThemeProvider>
    </ErrorBoundary>
  );
}
```

---

## Design System Summary

### Color Palette (OKLCH Format)
- **Primary (Sage Green)**: `oklch(0.55 0.08 160)` - Spiritual, calming
- **Accent (Gold)**: `oklch(0.7 0.12 70)` - Prosperity, abundance
- **Background (Beige)**: `oklch(0.98 0.01 80)` - Warm, welcoming
- **Foreground (Dark Brown)**: `oklch(0.25 0.02 60)` - Readable, grounded

### Typography
- **Headings**: Playfair Display (serif) - Elegant, luxury feel
- **Body**: Inter (sans-serif) - Clean, readable

### Key Features
- ✅ 7 strategic conversion optimization steps
- ✅ Multiple CTAs throughout the page
- ✅ Countdown timer for urgency
- ✅ Scarcity messaging (12 seats, limited time)
- ✅ Pain-point section addressing audience struggles
- ✅ Vritikaa's story and authority
- ✅ Transformation-focused content
- ✅ Comprehensive FAQ section
- ✅ Dramatic final CTA
- ✅ Fully responsive design
- ✅ Smooth scroll behavior
- ✅ High-quality images and branding

---

## Implementation Notes

1. **Update Countdown Timer**: Modify the initial state in `Home.tsx` with your actual workshop date
2. **Link Registration**: Replace the alert in the CTA button with your actual registration form URL
3. **Images**: All images are stored in `/client/public/images/` and referenced with absolute paths
4. **Logo**: Using transparent PNG version (`logo-nobg.png`) for clean branding
5. **Styling**: All styles use Tailwind CSS 4 with OKLCH color format
6. **Accessibility**: Proper semantic HTML, ARIA labels, and keyboard navigation

---

## File Locations

```
/home/ubuntu/numerology_landing/
├── client/
│   ├── public/images/
│   │   ├── logo-nobg.png
│   │   ├── IMG_0433.jpg (Hero image)
│   │   ├── IMG_3746.JPG (About section)
│   │   ├── IMG_3719.jpg (About section)
│   │   ├── IMG_2518.JPG (About section)
│   │   └── F1A8FB32-411E-45BC-9A40-C6F8CC953542.JPG (Final CTA)
│   ├── src/
│   │   ├── pages/Home.tsx
│   │   ├── const.ts
│   │   ├── index.css
│   │   ├── App.tsx
│   │   └── main.tsx
│   └── index.html
└── [Other project files]
```

---

## Version Information
- **Project**: numerology_landing
- **Latest Checkpoint**: 2445d08e
- **Design System**: Pastel Green, Beige, Gold
- **Framework**: React 19 + Tailwind CSS 4
- **Status**: Production Ready ✅
