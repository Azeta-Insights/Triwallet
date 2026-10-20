import React, { useMemo, useState } from 'react';
import { SafeAreaView, ScrollView, StatusBar, StyleSheet, Text, TouchableOpacity, View, Platform } from 'react-native';
import { LinearGradient } from 'expo-linear-gradient';
import { Ionicons } from '@expo/vector-icons';

type Currency = 'NGN' | 'USD' | 'GBP';
const rates: Record<Currency, number> = { NGN: 1, USD: 1585.20, GBP: 2054.45 }; // demo only; production must use approved live provider
const money = (v: number, c: Currency) => new Intl.NumberFormat('en-NG', { style: 'currency', currency: c, maximumFractionDigits: c === 'NGN' ? 0 : 2 }).format(v);
const actions = [['Send', 'arrow-up', 'Transfer securely'], ['Receive', 'arrow-down', 'Show account details'], ['Add money', 'add', 'Fund your wallet'], ['More', 'grid', 'All services']] as const;
const services = [['Electricity', 'flash', 'prepaid and postpaid'], ['Airtime', 'phone-portrait', 'all networks'], ['AI plans', 'sparkles', 'approved merchants'], ['Cowry', 'bus', 'Lagos bus top-up'], ['Train', 'train', 'ticket partners'], ['NGX Watch', 'trending-up', 'market monitoring'], ['Savings', 'lock-closed', 'goal-based pockets'], ['Loans', 'cash', 'eligible users only']] as const;
const tx = [['Electricity payment', '- ₦12,500', 'Today, 19:42'], ['Wallet funding', '+ ₦250,000', 'Today, 13:05'], ['Airtime', '- ₦5,000', 'Yesterday, 08:12']];

export default function App() {
  const [currency, setCurrency] = useState<Currency>('NGN');
  const [hidden, setHidden] = useState(false);
  const ngn = 425000;
  const value = useMemo(() => currency === 'NGN' ? ngn : ngn / rates[currency], [currency]);

  return (
    <View style={s.webContainer}>
      <SafeAreaView style={s.safe}>
        <StatusBar barStyle="light-content" />
        <ScrollView contentContainerStyle={s.page}>
          <View style={s.head}>
            <View>
              <Text style={s.hello}>Good evening, Stephen</Text>
              <Text style={s.sub}>Your money, clearly organised</Text>
            </View>
            <TouchableOpacity style={s.bell}>
              <Ionicons name="notifications-outline" size={20} color="#E9FFF7" />
            </TouchableOpacity>
          </View>
          <LinearGradient colors={['#0E6B54', '#0B3E34']} style={s.card}>
            <View style={s.row}>
              <Text style={s.label}>AVAILABLE BALANCE</Text>
              <TouchableOpacity onPress={() => setHidden(!hidden)}>
                <Ionicons name={hidden ? 'eye-off-outline' : 'eye-outline'} size={20} color="#C9F7E8" />
              </TouchableOpacity>
            </View>
            <Text style={s.balance}>{hidden ? '••••••' : money(value, currency)}</Text>
            <Text style={s.rate}>{currency === 'NGN' ? 'Primary spendable balance' : `Indicative value at ₦${rates[currency].toLocaleString()}/${currency}`}</Text>
            <View style={s.tabs}>
              {(['NGN', 'USD', 'GBP'] as Currency[]).map(c => (
                <TouchableOpacity key={c} onPress={() => setCurrency(c)} style={[s.tab, currency === c && s.tabOn]}>
                  <Text style={[s.tabText, currency === c && s.tabTextOn]}>{c}</Text>
                </TouchableOpacity>
              ))}
            </View>
          </LinearGradient>
          <View style={s.actions}>
            {actions.map(([t, i, d]) => (
              <TouchableOpacity key={t} style={s.action}>
                <View style={s.actionIcon}>
                  <Ionicons name={i as any} size={21} color="#09654E" />
                </View>
                <Text style={s.actionTitle}>{t}</Text>
                <Text style={s.actionDesc}>{d}</Text>
              </TouchableOpacity>
            ))}
          </View>
          <View style={s.sectionHead}>
            <Text style={s.section}>Services</Text>
            <Text style={s.link}>See all</Text>
          </View>
          <View style={s.grid}>
            {services.map(([t, i, d]) => (
              <TouchableOpacity key={t} style={s.service}>
                <View style={s.serviceIcon}>
                  <Ionicons name={i as any} size={22} color="#0A6C53" />
                </View>
                <Text style={s.serviceTitle}>{t}</Text>
                <Text style={s.serviceDesc}>{d}</Text>
              </TouchableOpacity>
            ))}
          </View>
          <View style={s.banner}>
            <Ionicons name="shield-checkmark" size={25} color="#056044" />
            <View style={{ flex: 1 }}>
              <Text style={s.bannerT}>Security centre</Text>
              <Text style={s.bannerD}>Biometrics on • Device trusted • KYC verified</Text>
            </View>
            <Ionicons name="chevron-forward" size={20} color="#61736D" />
          </View>
          <View style={s.sectionHead}>
            <Text style={s.section}>Recent activity</Text>
            <Text style={s.link}>View all</Text>
          </View>
          <View style={s.txBox}>
            {tx.map(([a, b, c], idx) => (
              <View key={a} style={[s.tx, idx < tx.length - 1 && s.txLine]}>
                <View style={s.txIcon}>
                  <Ionicons name={b.startsWith('+') ? 'arrow-down' : 'arrow-up'} size={18} color={b.startsWith('+') ? '#078458' : '#B85135'} />
                </View>
                <View style={{ flex: 1 }}>
                  <Text style={s.txT}>{a}</Text>
                  <Text style={s.txD}>{c}</Text>
                </View>
                <Text style={[s.txV, b.startsWith('+') && { color: '#078458' }]}>{b}</Text>
              </View>
            ))}
          </View>
          <Text style={s.disclaimer}>Prototype data only. Foreign currency figures are indicative conversions, not USD/GBP wallets.</Text>
        </ScrollView>
      </SafeAreaView>
    </View>
  );
}

const s = StyleSheet.create({
  webContainer: { flex: 1, height: Platform.OS === 'web' ? '100vh' : '100%', backgroundColor: '#081D19' },
  safe: { flex: 1, backgroundColor: '#081D19' },
  page: { padding: 18, paddingBottom: 40, backgroundColor: '#F4F7F5' },
  head: { margin: -18, marginBottom: 18, padding: 20, paddingTop: 22, backgroundColor: '#081D19', flexDirection: 'row', justifyContent: 'space-between', alignItems: 'center' },
  hello: { color: '#fff', fontSize: 20, fontWeight: '700' },
  sub: { color: '#9AC0B5', fontSize: 13, marginTop: 4 },
  bell: { padding: 10, borderWidth: 1, borderColor: '#285248', borderRadius: 14 },
  card: { padding: 20, borderRadius: 24 },
  row: { flexDirection: 'row', justifyContent: 'space-between' },
  label: { fontSize: 11, letterSpacing: 1.3, color: '#C9F7E8', fontWeight: '700' },
  balance: { fontSize: 34, color: '#fff', fontWeight: '800', marginTop: 12 },
  rate: { color: '#B5D9CE', fontSize: 12, marginTop: 5 },
  tabs: { flexDirection: 'row', marginTop: 20, backgroundColor: '#0A332B', padding: 4, borderRadius: 13 },
  tab: { flex: 1, padding: 9, alignItems: 'center', borderRadius: 10 },
  tabOn: { backgroundColor: '#E9FFF7' },
  tabText: { color: '#9BCABD', fontWeight: '700' },
  tabTextOn: { color: '#07533F' },
  actions: { flexDirection: 'row', gap: 8, marginTop: 16 },
  action: { flex: 1, alignItems: 'center' },
  actionIcon: { height: 44, width: 44, borderRadius: 15, backgroundColor: '#DAF3EA', alignItems: 'center', justifyContent: 'center' },
  actionTitle: { fontSize: 12, fontWeight: '700', marginTop: 7, color: '#172B25' },
  actionDesc: { display: 'none' },
  sectionHead: { flexDirection: 'row', justifyContent: 'space-between', alignItems: 'center', marginTop: 25, marginBottom: 12 },
  section: { fontSize: 18, fontWeight: '800', color: '#172B25' },
  link: { fontSize: 12, color: '#0A6C53', fontWeight: '700' },
  grid: { flexDirection: 'row', flexWrap: 'wrap', gap: 10 },
  service: { width: '48%', backgroundColor: '#fff', padding: 14, borderRadius: 18, borderWidth: 1, borderColor: '#E4EBE8' },
  serviceIcon: { height: 40, width: 40, borderRadius: 13, backgroundColor: '#E7F6F0', alignItems: 'center', justifyContent: 'center' },
  serviceTitle: { fontWeight: '800', color: '#182923', marginTop: 10 },
  serviceDesc: { fontSize: 11, color: '#788781', marginTop: 3 },
  banner: { marginTop: 20, padding: 15, backgroundColor: '#DFF6EC', borderRadius: 18, flexDirection: 'row', gap: 12, alignItems: 'center' },
  bannerT: { fontWeight: '800', color: '#143C31' },
  bannerD: { fontSize: 11, color: '#587068', marginTop: 3 },
  txBox: { backgroundColor: '#fff', borderRadius: 19, paddingHorizontal: 15 },
  tx: { flexDirection: 'row', alignItems: 'center', paddingVertical: 14, gap: 12 },
  txLine: { borderBottomWidth: 1, borderBottomColor: '#EDF1EF' },
  txIcon: { height: 36, width: 36, borderRadius: 12, backgroundColor: '#F0F5F3', alignItems: 'center', justifyContent: 'center' },
  txT: { fontWeight: '700', color: '#1D302A' },
  txD: { fontSize: 11, color: '#7B8984', marginTop: 3 },
  txV: { fontWeight: '800', color: '#2B3834' },
  disclaimer: { fontSize: 10, color: '#81908B', textAlign: 'center', marginTop: 18 }
});
